---
name: fullstack-security-auditor
description: "MANDATORY - Must execute view_file on this skill before handling authentication, authorization, user input sanitization, security headers, or sensitive secrets. Enterprise OWASP Top 10 security and DevSecOps."
---

# 🛡️ Fullstack Security Auditor — Enterprise OWASP & DevSecOps Architecture

This skill provides an enterprise-grade defense framework for web applications, REST/RPC APIs, authentication layers, and database operations, enforcing OWASP Top 10 mitigations, strict input sanitization, cryptography standards, and secret management.

---

# HARD BANS — UNFORGIVABLE SECURITY ANTI-PATTERNS

The following security vulnerabilities are **STRICTLY PROHIBITED**:

### 1. Storing JWTs/Tokens in `localStorage` or `sessionStorage` is BANNED
- ❌ **Prohibited:** Persisting authentication tokens or session IDs inside client-side Web Storage (`localStorage.setItem('auth_token', token)`).
- 💣 **Failure Mode:** Any cross-site scripting (XSS) vulnerability in any third-party script or dependency can immediately read all stored tokens and exfiltrate accounts.
- ✅ **Mandatory:** Authentication tokens must reside exclusively inside `HttpOnly`, `Secure`, `SameSite=Lax` (or `Strict`) cookies that cannot be accessed via JavaScript.

### 2. IDOR-Prone Database Mutations are BANNED
- ❌ **Prohibited:** Executing updates or deletes relying solely on resource IDs without verifying owner tenant context (e.g., `DELETE FROM documents WHERE id = ${params.id}`).
- 💣 **Failure Mode:** An authenticated user can alter the numeric or UUID parameter in the URL and modify, delete, or inspect other users' private documents (Insecure Direct Object Reference).
- ✅ **Mandatory:** Every mutation and fetch query must enforce user/tenant binding: `WHERE id = ${params.id} AND user_id = ${currentUser.id}`.

### 3. Exposing Sequential Auto-Increment IDs in Public URLs is BANNED
- ❌ **Prohibited:** Exposing raw sequential database integer IDs in public routes (e.g., `/api/invoices/1042`, `/user/48`).
- 💣 **Failure Mode:** Enables automated enumeration attacks. Competitors can scrape all company invoices and deduce customer acquisition rates.
- ✅ **Mandatory:** Public resource locators must use non-sequential cryptographically random keys: `UUIDv7`, `ULID`, or `Nanoid`.

### 4. Permissive CORS (`*` with Credentials) is BANNED
- ❌ **Prohibited:** Setting `Access-Control-Allow-Origin: *` while configuring `Access-Control-Allow-Credentials: true`.
- 💣 **Failure Mode:** Either rejected outright by modern browsers or permits third-party websites to forge authenticated cross-origin requests.
- ✅ **Mandatory:** Maintain an explicit whitelist of trusted production and staging origins.

### 5. Logging Sensitive PII, Passwords or Keys is BANNED
- ❌ **Prohibited:** Dumping entire raw request payloads or error objects to standard output (e.g., `console.log("Login Payload:", req.body)`).
- 💣 **Failure Mode:** Passwords, API tokens, national IDs, and credit cards stream into centralized logging platforms (Datadog, CloudWatch), violating GDPR/KVKK and leaking credentials.
- ✅ **Mandatory:** Sanitize and redact sensitive keys (`password`, `token`, `secret`, `cvv`) through a structured logger before emitting logs.

---

# ACTIVE OWASP DEFENSE STANDARDS

### 1. SQL & NoSQL Injection Defense
- Raw string concatenation in queries (`SELECT * FROM users WHERE id = '${id}'`) is **STRICTLY FORBIDDEN**.
- All database queries must execute through typed ORMs (Drizzle / Prisma) or parameterized SQL bindings (`$1, $2`).

### 2. XSS (Cross-Site Scripting) Defense
- All dynamic user-submitted HTML must be sanitized before rendering into the DOM:
  - React / Next.js: Raw `dangerouslySetInnerHTML` is prohibited unless explicitly sanitized via `DOMPurify.sanitize(content)`.
  - Raw unescaped user data must never be directly injected into markup; preserve React's default string escaping and `textContent` bindings.

### 3. Cryptographic Authentication (Argon2id Baseline)
- Passwords must never be stored in plain text or with obsolete hashes (MD5, SHA1, SHA256 without salting).
- Baseline: **Argon2id** or **Bcrypt (work factor >= 12)**:
```typescript
import argon2 from "argon2";

export async function hashPassword(password: string): Promise<string> {
  return await argon2.hash(password, { type: argon2.argon2id });
}

export async function verifyPassword(hash: string, plain: string): Promise<boolean> {
  return await argon2.verify(hash, plain);
}
```

### 4. HTTP Security Headers
Injected at middleware or reverse proxy (`next.config.js` / Cloudflare) layers:
```typescript
export const securityHeaders = [
  { key: "Content-Security-Policy", value: "default-src 'self'; script-src 'self' 'unsafe-inline' 'unsafe-eval'; style-src 'self' 'unsafe-inline'; img-src 'self' data: https:; font-src 'self' data:;" },
  { key: "X-Frame-Options", value: "DENY" },
  { key: "X-Content-Type-Options", value: "nosniff" },
  { key: "Referrer-Policy", value: "strict-origin-when-cross-origin" },
  { key: "Permissions-Policy", value: "camera=(), microphone=(), geolocation=()" },
  { key: "Strict-Transport-Security", value: "max-age=63072000; includeSubDomains; preload" }
];
```

### 5. DevSecOps & Secret Protection
- **Zero Hard-Coded Credentials:** Committing private API keys (`sk_live_...`, `AIzaSy...`), database credentials, or private certificates into source code is STRICTLY FORBIDDEN.
- **Environment Variable Isolation:** `.env` and local secrets must always be tracked inside `.gitignore`. Only a sanitized `.env.example` template is maintained in version control.
