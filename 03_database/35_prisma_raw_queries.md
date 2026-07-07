# 35. When and how do you use raw queries in Prisma? (Senior)

Prisma's generated API covers most needs, but complex SQL (window functions, CTEs, DB-specific features) may require **raw queries**. Prisma provides safe escape hatches.

**`$queryRaw`** — returns rows; use a **tagged template** so values are parameterized (SQL-injection safe):

```ts
const email = "ada@example.com";
const users = await prisma.$queryRaw<User[]>`
  SELECT * FROM "User" WHERE email = ${email}
`; // ${email} is bound as a parameter, NOT string-interpolated
```

**`$executeRaw`** — for writes (returns affected row count):

```ts
await prisma.$executeRaw`UPDATE "User" SET active = false WHERE last_login < ${cutoff}`;
```

**Dynamic SQL** — compose safely with `Prisma.sql` / `Prisma.join`:

```ts
import { Prisma } from "@prisma/client";
const ids = [1, 2, 3];
await prisma.$queryRaw(Prisma.sql`SELECT * FROM "User" WHERE id IN (${Prisma.join(ids)})`);
```

**⚠️ Danger:** `$queryRawUnsafe`/`$executeRawUnsafe` take a plain string — **never** interpolate user input into them (injection risk). Prefer the tagged-template versions.

**Key point:** drop to `$queryRaw`/`$executeRaw` for SQL the typed API can't express, always using **tagged templates** (or `Prisma.sql`/`Prisma.join`) so inputs are parameterized; avoid the `*Unsafe` variants with untrusted input, and cast the result type since raw results aren't inferred.
