# 12. What is a race condition in a database? (Mid)

A **race condition** occurs when two operations run concurrently and the final result depends on **timing** — often causing a **lost update**.

**Classic bug — read-modify-write:**

```ts
// Two requests run this at the same time, stock = 1
const p = await db.query("SELECT stock FROM products WHERE id = 1"); // both read 1
if (p.stock > 0) {
  await db.query("UPDATE products SET stock = 0 WHERE id = 1"); // both sell → oversold!
}
```

Both see `stock = 1`, both sell → **overselling**.

**Fixes:**

```sql
-- 1. Atomic update (let the DB do the check)
UPDATE products SET stock = stock - 1 WHERE id = 1 AND stock > 0;

-- 2. Row lock
SELECT stock FROM products WHERE id = 1 FOR UPDATE;

-- 3. Optimistic version check (see locking question)
```

**Key point:** never do check-then-act across separate queries under concurrency. Make the operation **atomic** or **locked**. See [flash-sale overselling] use case.
