# 28. How do you perform CRUD with Prisma Client? (Junior)

Prisma Client exposes a **typed method per model** with a consistent, fluent query API.

```ts
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

// CREATE
const user = await prisma.user.create({
  data: { email: "ada@example.com", name: "Ada" },
});

// READ
const one = await prisma.user.findUnique({ where: { id: 1 } });
const many = await prisma.user.findMany({
  where: { name: { contains: "Ada" } },
  orderBy: { createdAt: "desc" },
  take: 10, // limit
  skip: 20, // offset (pagination)
  select: { id: true, email: true }, // pick fields
});

// UPDATE
await prisma.user.update({ where: { id: 1 }, data: { name: "Ada L." } });

// UPSERT
await prisma.user.upsert({
  where: { email: "ada@example.com" },
  create: { email: "ada@example.com", name: "Ada" },
  update: { name: "Ada" },
});

// DELETE
await prisma.user.delete({ where: { id: 1 } });

// Bulk
await prisma.user.updateMany({ where: { name: null }, data: { name: "N/A" } });
```

**Notes:** results are fully typed; `select`/`include` shape the return type; filters support `contains`, `in`, `gt`, `AND`/`OR`, etc.

**Key point:** Prisma Client gives each model typed CRUD methods (`create`, `findUnique`/`findMany`, `update`, `upsert`, `delete`, and `*Many` bulk variants) with a fluent options object for `where`, `orderBy`, pagination (`take`/`skip`), and field selection — all type-checked.
