---
name: modern-data-engineer
description: "MANDATORY - Must execute view_file on this skill before creating or modifying database schemas, SQL queries, ORM models, migrations, or vector pipelines. Drizzle ORM, Prisma, PostgreSQL, pgvector, and connection pooling."
---

# 🗄️ Modern Data Engineer — Relational, Serverless & Vector Data Architecture

This skill provides an authoritative guide for building type-safe, high-concurrency, vector-enabled, and serverless-ready database architectures utilizing **Drizzle ORM, Prisma, PostgreSQL, MySQL, and pgvector**.

---

# HARD BANS — UNFORGIVABLE DATABASE ANTI-PATTERNS

The following database practices are **STRICTLY PROHIBITED**:

### 1. Unindexed Foreign Keys are BANNED
- ❌ **Prohibited:** Creating relation columns without indexes (e.g., `userId: uuid().references(() => users.id)` with no dedicated index).
- 💣 **Failure Mode:** PostgreSQL does NOT index foreign keys by default. Deleting or updating a parent record causes an exclusive table-level lock and sequential scan of the child table, freezing concurrent queries.
- ✅ **Mandatory:** Every foreign key column must be explicitly accompanied by an index (e.g., `index("idx_orders_user_id").on(table.userId)`).

### 2. In-Memory Client-Side Filtering/Sorting is BANNED
- ❌ **Prohibited:** Fetching broad records from the database and using JavaScript array methods (`.filter()`, `.sort()`) in Node.js memory.
- 💣 **Failure Mode:** Sucking 100k rows across the wire saturates network throughput, exhausts server memory, and bypasses database index acceleration.
- ✅ **Mandatory:** Push all filtering (`WHERE`), ordering (`ORDER BY`), and pagination (`LIMIT/OFFSET` or keyset cursor) directly down to the SQL engine.

### 3. Non-Timezoned `TIMESTAMP` Columns are BANNED
- ❌ **Prohibited:** Defining timestamp columns without explicit time zone support (e.g., `timestamp("created_at")` without `{ withTimezone: true }`).
- 💣 **Failure Mode:** Ambiguity across server regions, daylight saving time shifts, and client conversions corrupts chronological sorting and audit trails.
- ✅ **Mandatory:** Always declare `timestamp("created_at", { withTimezone: true })` (`TIMESTAMPTZ`) and enforce UTC storage across all tables.

### 4. Unpartitioned Multi-Tenant Vector Search is BANNED
- ❌ **Prohibited:** Executing `pgvector` HNSW/IVFFlat similarity searches without strict tenant isolation filters.
- 💣 **Failure Mode:** High-dimensional vector searches without pre-filtering leak Tenant A's private documents into Tenant B's retrieval pipeline if vector similarity is high.
- ✅ **Mandatory:** Every vector search query must enforce hard composite partitioning: `WHERE tenant_id = current_tenant AND ...` to isolate retrieval space.

### 5. Direct Unpooled Serverless DB Connections are BANNED
- ❌ **Prohibited:** Connecting directly to standard PostgreSQL port 5432 from stateless serverless environments (Next.js App Router, Edge/Lambda handlers).
- 💣 **Failure Mode:** Each serverless invocation spawns new connection threads. A sudden surge of 100 concurrent visitors immediately triggers `FATAL: too many connections for role`.
- ✅ **Mandatory:** Route all serverless connections through a managed transaction-mode connection pooler (PgBouncer, Neon Serverless Pooler, Supabase Pooler on port 6543).

### 6. Floating-Point Columns for Currency are BANNED
- ❌ **Prohibited:** Storing monetary amounts in `REAL`, `FLOAT`, or `DOUBLE PRECISION` columns.
- 💣 **Failure Mode:** Inherent binary floating-point representation drift accumulates financial calculation discrepancy.
- ✅ **Mandatory:** Store all monetary values as `INTEGER` representing the smallest currency unit (e.g., cents), or use `NUMERIC(12, 2)` / `DECIMAL`.

---

# ARCHITECTURAL STANDARDS

### 1. Modern ORM & Schema Design (Drizzle ORM & Prisma)
Database schemas must be designed strictly type-safe (End-to-End Type Safety):
```typescript
import { pgTable, uuid, text, timestamp, integer, index } from "drizzle-orm/pg-core";

export const users = pgTable("users", {
  id: uuid("id").defaultRandom().primaryKey(),
  email: text("email").notNull().unique(),
  role: text("role", { enum: ["user", "admin", "lead"] }).default("user").notNull(),
  createdAt: timestamp("created_at", { withTimezone: true }).defaultNow().notNull(),
  updatedAt: timestamp("updated_at", { withTimezone: true }).defaultNow().notNull(),
});

export const orders = pgTable("orders", {
  id: uuid("id").defaultRandom().primaryKey(),
  userId: uuid("user_id").references(() => users.id, { onDelete: "cascade" }).notNull(),
  totalCents: integer("total_cents").notNull(), // Integer cent precision
  status: text("status", { enum: ["pending", "paid", "failed"] }).default("pending").notNull(),
  createdAt: timestamp("created_at", { withTimezone: true }).defaultNow().notNull(),
}, (table) => [
  index("idx_orders_user_status_created").on(table.userId, table.status, table.createdAt.desc())
]);
```

### 2. Vector & AI Data Architecture (`pgvector` & RAG)
Standardize semantic search and vector storage using `pgvector`:
```sql
CREATE EXTENSION IF NOT EXISTS vector;

CREATE TABLE document_chunks (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    tenant_id UUID NOT NULL,
    document_id UUID NOT NULL,
    content TEXT NOT NULL,
    metadata JSONB DEFAULT '{}'::jsonb,
    embedding VECTOR(1536) -- OpenAI text-embedding-3 / Gemini dimensions
);

-- Pre-filtered HNSW Index
CREATE INDEX idx_document_embedding_hnsw 
ON document_chunks 
USING hnsw (embedding vector_cosine_ops)
WITH (m = 16, ef_construction = 64);
```

### 3. Serverless Connection Pooling & ACID Transactions
Multi-table mutations and balance deductions must execute inside `db.transaction()` with row-level pessimistic locks:
```typescript
await db.transaction(async (tx) => {
  // 1. Pessimistic row locking for concurrency safety
  const [product] = await tx.select().from(products).where(eq(products.id, productId)).for("update");
  if (product.stock < quantity) throw new Error("Insufficient stock available.");

  // 2. Decrement stock and insert order record atomically
  await tx.update(products).set({ stock: product.stock - quantity }).where(eq(products.id, productId));
  await tx.insert(orders).values({ userId, totalCents, status: "paid" });
});
```

### 4. Indexing & Query Optimization
- **Zero N+1 Queries:** Executing queries inside iteration loops is strictly prohibited. Use Drizzle relational queries (`with: { relation: true }`) or SQL `JOIN / WHERE IN`.
- **Composite Indexes:** Filter and sorting columns must be bound into single composite B-Tree indexes matching query patterns.
- **EXPLAIN ANALYZE Audit:** Any critical query exceeding 50ms must be evaluated with `EXPLAIN (ANALYZE, BUFFERS)` to eliminate sequential table scans.
