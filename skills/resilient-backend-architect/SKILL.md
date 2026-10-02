---
name: resilient-backend-architect
description: "MANDATORY - Must execute view_file on this skill before writing any backend, API, service, or server route code. Defensive, high-concurrency backend, rate limiting, quota guards, idempotency keys, and Zod schemas."
---

# 🏗️ Resilient Backend Architect — Defensive & Scale-Ready Backend Engineering

This skill strictly prohibits naive "happy-path-only" API implementations. It enforces high concurrency safety, cost and quota protection, distributed rate limiting, idempotency, and graceful degradation across all backend services, route handlers, and serverless architectures.

---

# HARD BANS — UNFORGIVABLE BACKEND ANTI-PATTERNS

The following patterns are **STRICTLY PROHIBITED** across all backend and API code:

### 1. In-Memory State in Serverless Runtimes is BANNED
- ❌ **Prohibited:** Storing mutable module-level state (e.g., `let activeUsers = {}`, `let rateLimitCounter = 0`, `let cache = new Map()`) inside Next.js Route Handlers, AWS Lambdas, or Edge functions.
- 💣 **Failure Mode:** Serverless instances spin up and down unpredictably. State is lost on cold starts, counters reset, and rate limiting fails across concurrent instances.
- ✅ **Mandatory:** All persistent and shared state must reside in an external distributed store (Redis / Upstash) or database.

### 2. Naked `SELECT *` & Unbounded Queries are BANNED
- ❌ **Prohibited:** Executing queries without explicit limits (e.g., `SELECT * FROM orders WHERE status = 'pending'`).
- 💣 **Failure Mode:** When a table grows to 50,000+ rows, a single unbounded request consumes gigabytes of RAM, triggers Out-Of-Memory (OOM) crashes, and saturates database I/O.
- ✅ **Mandatory:** Every list endpoint must enforce a strict `LIMIT` (maximum 100) and implement keyset/cursor or offset pagination. Select only needed columns.

### 3. Blind Catch-All Error Swallowing is BANNED
- ❌ **Prohibited:** Writing empty or unclassified try/catch blocks (e.g., `catch (e) { return res.json({ error: "Something went wrong" }) }`).
- 💣 **Failure Mode:** Hides database outages, syntax bugs, and network partition failures. Debugging becomes impossible in production.
- ✅ **Mandatory:** Log structured error details server-side (`console.error` with error type, stack, and context) and return standardized RFC 7807 problem details to the client without leaking internal infrastructure details.

### 4. Naked Runtime `process.env` Access is BANNED
- ❌ **Prohibited:** Accessing raw environment variables directly throughout business logic (e.g., `const key = process.env.STRIPE_SECRET_KEY`).
- 💣 **Failure Mode:** If an environment variable is missing, undefined, or malformed, the application crashes silently at runtime when a user hits that specific branch.
- ✅ **Mandatory:** Validate all environment variables at startup using a centralized Zod schema (`env.ts` / `t3-env` pattern). Fail fast on deployment if variables are invalid.

### 5. Unbounded External Network Requests are BANNED
- ❌ **Prohibited:** Calling external APIs without explicit timeouts (e.g., `await fetch("https://api.openai.com/...")`).
- 💣 **Failure Mode:** If an external vendor experiences high latency, incoming connections accumulate, thread pools exhaust, and the entire server freezes.
- ✅ **Mandatory:** Every outgoing fetch must attach an `AbortSignal.timeout(8000)` (or max 15s for long operations) with dedicated fallback handling.

### 6. Returning HTTP 200 for Failed Operations is BANNED
- ❌ **Prohibited:** Returning status code 200 OK with a body like `{ success: false, error: "Validation failed" }`.
- 💣 **Failure Mode:** API gateways, reverse proxies, uptime checkers, and client caching mechanisms treat failures as healthy responses, corrupting analytics and breaking error boundaries.
- ✅ **Mandatory:** Adhere strictly to semantic HTTP status codes: `400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found`, `422 Unprocessable Content`, `429 Too Many Requests`, and `500 Internal Server Error`.

---

# THE 7-LAYER RESILIENCE PIPELINE

Every mutation endpoint and business-critical route must progress through these defense layers:

```
[Incoming Client Request]
            │
            ▼
 1. [Rate Limiter & Bot Guard]  ➔ (Sliding Window via Redis / Upstash)
            │
            ▼
 2. [Strict Zod DTO Validation]➔ (Sanitize Body, Query & URL Params)
            │
            ▼
 3. [Idempotency Key Check]     ➔ (Prevent Duplicate Charges / Mutations)
            │
            ▼
 4. [Quota & Token Budget Guard]➔ (Track API Costs & Tenant Resource Quotas)
            │
            ▼
 5. [Core Business Logic]       ➔ (Clean Architecture, Typed DTOs, Single SSOT)
            │
            ▼
 6. [Resilient Fetch & DB]      ➔ (Timeout AbortController + Circuit Breakers)
            │
            ▼
 7. [Structured JSON Envelope]  ➔ (RFC 7807 Standard Error & Success Formats)
```

---

# IMPLEMENTATION STANDARDS

### 1. Strict Runtime Validation & DTOs via Zod
Every piece of data entering or leaving an endpoint must be validated through strict Zod schemas:
```typescript
import { z } from "zod";

export const CreateOrderSchema = z.object({
  productId: z.string().uuid("Invalid product ID format"),
  quantity: z.number().int().min(1).max(100),
  currency: z.enum(["USD", "EUR", "TRY"]),
  shippingAddress: z.object({
    street: z.string().min(5).max(200),
    city: z.string().min(2).max(50),
    postalCode: z.string().regex(/^\d{5}$/, "Invalid postal code")
  })
}).strict(); // Strip and reject any undeclared fields

export type CreateOrderDTO = z.infer<typeof CreateOrderSchema>;
```

### 2. Idempotency & Distributed Locking
Every financial or state-altering `POST/PUT` mutation must honor an `Idempotency-Key` header:
```typescript
export async function handleIdempotentMutation(key: string, fn: () => Promise<any>) {
  const cachedResponse = await redis.get(`idempotency:${key}`);
  if (cachedResponse) {
    return JSON.parse(cachedResponse); // Return original result without re-executing
  }

  const result = await fn();
  await redis.set(`idempotency:${key}`, JSON.stringify(result), "EX", 86400); // 24-hour TTL
  return result;
}
```

### 3. Network Timeouts via AbortController
No outgoing network request may hang indefinitely:
```typescript
export async function fetchWithTimeout(url: string, options: RequestInit, timeoutMs = 8000) {
  const controller = new AbortController();
  const timeoutId = setTimeout(() => controller.abort(), timeoutMs);

  try {
    const response = await fetch(url, { ...options, signal: controller.signal });
    return response;
  } catch (err: any) {
    if (err.name === "AbortError") {
      throw new Error(`External service timed out (${timeoutMs}ms limit exceeded).`);
    }
    throw err;
  } finally {
    clearTimeout(timeoutId);
  }
}
```

### 4. Quota & Token Budget Guard
Protect against runaway LLM or external API costs:
```typescript
export async function enforceTokenBudget(orgId: string, estimatedTokens: number) {
  const currentUsage = await redis.incrby(`usage:${orgId}:${currentMonth()}`, estimatedTokens);
  const monthlyLimit = await getOrgMonthlyTokenLimit(orgId);

  if (currentUsage > monthlyLimit) {
    throw new QuotaExceededError("Monthly token budget exhausted. Please upgrade your plan.");
  }
}
```

---

# STANDARDIZED API ENVELOPE (RFC 7807 COMPLIANT)

### Success Response (200 / 201):
```json
{
  "success": true,
  "statusCode": 200,
  "data": {
    "orderId": "ord_98a7b6c5",
    "status": "processing"
  },
  "meta": {
    "timestamp": "2026-09-25T14:00:00Z",
    "requestId": "req_xyz123"
  }
}
```

### Error Response (RFC 7807 Format - 4xx / 5xx):
```json
{
  "success": false,
  "statusCode": 422,
  "error": {
    "code": "VALIDATION_FAILED",
    "message": "Payload validation failed.",
    "details": [
      { "field": "quantity", "issue": "Quantity cannot exceed 100." }
    ]
  },
  "meta": {
    "timestamp": "2026-09-25T14:00:00Z",
    "requestId": "req_xyz123"
  }
}
```
*Never leak raw SQL queries, file system paths, or internal server stack traces to clients.*
