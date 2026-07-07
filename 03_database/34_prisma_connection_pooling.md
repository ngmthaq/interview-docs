# 34. How do you manage Prisma connections and pooling? (Senior)

Prisma Client maintains an internal **connection pool**. Mismanaging it — especially in **serverless** — is a common production pitfall.

**Instantiate the client once** (a singleton):

```ts
// Avoid `new PrismaClient()` per request — it exhausts DB connections
const globalForPrisma = globalThis as unknown as { prisma?: PrismaClient };
export const prisma = globalForPrisma.prisma ?? new PrismaClient();
if (process.env.NODE_ENV !== "production") globalForPrisma.prisma = prisma;
```

**Pool size** — tune via the connection string:

```
postgresql://...?connection_limit=10&pool_timeout=20
```

**The serverless problem:**

- Each serverless instance opens its own pool; under load, hundreds of instances can **exhaust** the database's max connections.
- **Solutions:**
  - An external pooler like **PgBouncer** (add `?pgbouncer=true`), or
  - **Prisma Accelerate** — a managed connection pool + global cache, or
  - The database's built-in pooler (e.g. Supabase/Neon pooled endpoint).

**Also:** call **`prisma.$disconnect()`** on shutdown in long-running apps; in serverless, reuse the client across invocations rather than disconnecting each time.

**Key point:** instantiate `PrismaClient` once (singleton) to avoid connection exhaustion, tune `connection_limit` in the URL, and in serverless put a pooler in front (PgBouncer, Prisma Accelerate, or the DB's pooled endpoint) since many short-lived instances otherwise overwhelm the database's connection limit.
