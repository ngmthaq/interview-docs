# 32. How do transactions work in Prisma? (Mid)

Prisma offers two transaction styles to run multiple operations **atomically** (all succeed or all roll back).

**1. Sequential array — `$transaction([...])`:**

```ts
// All run in one transaction; the array order is preserved
const [user, post] = await prisma.$transaction([
  prisma.user.create({ data: { email: "a@x.com" } }),
  prisma.post.create({ data: { title: "Hi", authorId: 1 } }),
]);
```

**2. Interactive transaction — `$transaction(async (tx) => ...)`:**

```ts
await prisma.$transaction(async (tx) => {
  const from = await tx.account.update({
    where: { id: 1 },
    data: { balance: { decrement: 100 } },
  });
  if (from.balance < 0) throw new Error("Insufficient funds"); // rolls back
  await tx.account.update({
    where: { id: 2 },
    data: { balance: { increment: 100 } },
  });
});
```

**Key facts:**

- Use the **array** form for independent writes; the **interactive** form when later steps depend on earlier results or need conditional logic.
- Any thrown error → **automatic rollback**.
- Set **`isolationLevel`** and a **`timeout`** in options; keep interactive transactions **short** (they hold a DB connection and locks).
- **Nested writes** (creating relations in one call) are already atomic without `$transaction`.

**Key point:** Prisma provides `$transaction([...])` for a batch of independent atomic writes and interactive `$transaction(async tx => ...)` when steps depend on each other — both roll back on any error; keep interactive transactions short to avoid holding connections/locks.
