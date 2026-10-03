---
name: ecommerce-payments-engine
description: "MANDATORY - Must execute view_file on this skill before handling payments, checkout, cart calculations, stock reservation, or order processing. Integer cent math, Stripe, Iyzico, and order state machines."
---

# 🛒 E-Commerce & Payments Engine — Financial Accuracy & Transaction Resilience

This skill ensures zero floating-point calculation errors in e-commerce workflows, eliminates inventory overselling and race conditions, integrates Stripe and İyzico payment gateways with cryptographic signature verification, and enforces strict order state machines.

---

# HARD BANS — UNFORGIVABLE E-COMMERCE ANTI-PATTERNS

The following practices are **STRICTLY PROHIBITED** across all e-commerce and checkout implementations:

### 1. Trusting Client-Provided Prices or Totals is BANNED
- ❌ **Prohibited:** Allowing the frontend payload to dictate `price`, `discount`, `taxAmount`, or `total` in checkout requests (e.g., `{ productId: "p1", price: 10 }`).
- 💣 **Failure Mode:** Any user can open DevTools and alter the payload, purchasing a $1,000 product for $1.
- ✅ **Mandatory:** The client sends ONLY `productId`, `quantity`, and optional validated voucher codes. All pricing, item sub-totals, discounts, taxes, and final totals must be recalculated exclusively on the server from authoritative database records.

### 2. Floating-Point Financial Arithmetic is BANNED
- ❌ **Prohibited:** Performing currency operations with standard JavaScript numbers (e.g., `itemPrice * 1.18` or `0.1 + 0.2`).
- 💣 **Failure Mode:** Binary precision drift (`$19.990000000000002`) causes discrepancies with payment processors, triggering transaction rejections and reconciliation chaos.
- ✅ **Mandatory:** Perform all financial calculations in integer cents (e.g., `$19.99` is represented as `1999` integer cents) or use `BigInt`.

### 3. Taking Payments Without Inventory Reservation is BANNED
- ❌ **Prohibited:** Charging a customer's card first, and then decrementing inventory stock afterwards.
- 💣 **Failure Mode:** If two users purchase the final unit simultaneously, both are charged, but one cannot be fulfilled (the classic overselling crisis).
- ✅ **Mandatory:** Atomically increment `reserved_stock` before redirecting to payment or generating PaymentIntents. If payment fails or times out within 15 minutes, automatically release the hold via background job.

### 4. Updating Order Status to "PAID" from Client Redirects is BANNED
- ❌ **Prohibited:** Marking an order as "paid" simply because a user landed on `/checkout/success?session_id=...`.
- 💣 **Failure Mode:** Malicious users can navigate directly to the success URL or replay sessions, falsely triggering order fulfillment without ever paying.
- ✅ **Mandatory:** Order status transitions to `paid` must happen **ONLY** inside the cryptographically signed webhook listener (`stripe.webhooks.constructEvent` or İyzico callback verification).

### 5. Storing Raw Card Details in Application Databases is BANNED
- ❌ **Prohibited:** Receiving or persisting raw Primary Account Numbers (PANs), CVVs, or card expiration dates in application payloads or database tables.
- 💣 **Failure Mode:** Direct violation of PCI-DSS compliance, exposing the company to catastrophic liability and severe regulatory penalties.
- ✅ **Mandatory:** Card data must go directly to payment gateway iframes/SDKs (Stripe Elements, İyzico Form). The backend receives only tokenized IDs (`pm_...`, `pi_...`).

---

# ARCHITECTURAL STANDARDS

### 1. Integer Cent Cart Engine
```typescript
export interface CartItem {
  productId: string;
  unitPriceCents: number; // e.g., $49.90 -> 4990 cents
  quantity: number;
  taxRatePercent: number; // e.g., 20 for 20% VAT
}

export function calculateOrderSummary(items: CartItem[], discountCents = 0, shippingCents = 0) {
  const subtotalCents = items.reduce((acc, item) => acc + item.unitPriceCents * item.quantity, 0);
  
  const taxCents = items.reduce((acc, item) => {
    const itemTotal = item.unitPriceCents * item.quantity;
    return acc + Math.round(itemTotal * (item.taxRatePercent / 100));
  }, 0);

  const totalCents = Math.max(0, subtotalCents + taxCents + shippingCents - discountCents);

  return { subtotalCents, taxCents, shippingCents, discountCents, totalCents };
}
```

### 2. Cryptographic Webhook Verification (Stripe Example)
```typescript
import Stripe from "stripe";
import { env } from "@/env"; // Validated startup Zod environment schema

const stripe = new Stripe(env.STRIPE_SECRET_KEY, { apiVersion: "2024-06-20" });

// Note: In Next.js App Router, extract rawBody using `await req.text()`; never parse JSON first
export async function handleStripeWebhook(rawBody: string | Buffer, signature: string) {
  let event: Stripe.Event;

  try {
    event = stripe.webhooks.constructEvent(rawBody, signature, env.STRIPE_WEBHOOK_SECRET);
  } catch (err: any) {
    throw new Error(`Webhook Signature Verification Failed: ${err.message}`);
  }

  if (event.type === "payment_intent.succeeded") {
    const paymentIntent = event.data.object as Stripe.PaymentIntent;
    const orderId = paymentIntent.metadata.orderId;
    await transitionOrderStatus(orderId, "paid", { transactionId: paymentIntent.id });
  }

  return { received: true };
}
```

### 3. Strict Order State Machine
Order statuses must strictly transition through validated paths:
```
[draft] ➔ [pending_payment] ➔ [paid] ➔ [processing] ➔ [shipped] ➔ [delivered] ➔ [completed]
   │               │            │
   ▼               ▼            ▼
[cancelled]   [failed]      [refunded]
```

```typescript
const VALID_TRANSITIONS: Record<string, string[]> = {
  draft: ["pending_payment", "cancelled"],
  pending_payment: ["paid", "failed", "cancelled"],
  paid: ["processing", "refunded"],
  processing: ["shipped", "refunded"],
  shipped: ["delivered"],
  delivered: ["completed", "refunded"],
  completed: ["refunded"],
  failed: ["pending_payment"],
  cancelled: [],
  refunded: []
};

export function validateStateTransition(current: string, next: string) {
  if (!VALID_TRANSITIONS[current]?.includes(next)) {
    throw new Error(`Illegal order state transition: ${current} -> ${next}`);
  }
}
```

### 4. Concurrency & Inventory Reservation
- When checkout initiates, increment `reserved_stock` atomically.
- If payment is not finalized within 15 minutes, a scheduled background cron releases the reservation back to available inventory.
- Final checkout execution utilizes `SELECT ... FOR UPDATE` or optimistic version locking (`version_id`) to completely prevent overselling.
