# 5. What is a transaction? (Junior)

A **transaction** is a unit of work that groups multiple operations so they execute as a **single, all-or-nothing** action.

```sql
BEGIN;                                   -- start
  INSERT INTO orders(user_id, total) VALUES (1, 50);
  UPDATE inventory SET stock = stock - 1 WHERE product_id = 9;
COMMIT;                                  -- make permanent
-- ROLLBACK;  -- or undo everything on error
```

**Lifecycle:** `BEGIN` → operations → `COMMIT` (save) or `ROLLBACK` (undo).

**Why use them:**

- Keep related changes consistent (order + inventory update must both happen).
- Recover cleanly from errors — partial failures are rolled back.

**Key point:** transactions give you **Atomicity** and **Isolation** from ACID. Keep them **short** — long transactions hold locks and hurt concurrency.
