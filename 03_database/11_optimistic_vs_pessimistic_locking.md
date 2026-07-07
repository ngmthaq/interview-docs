# 11. Optimistic vs Pessimistic locking? (Mid → Senior)

Both prevent **lost updates** when two transactions modify the same row, but with opposite strategies.

**Pessimistic** — lock the row up front; others wait.

```sql
BEGIN;
  SELECT * FROM products WHERE id = 1 FOR UPDATE; -- lock the row
  UPDATE products SET stock = stock - 1 WHERE id = 1;
COMMIT;
```

**Optimistic** — no lock; detect conflicts at write time using a **version** column.

```sql
-- read version = 5, then:
UPDATE products
SET stock = stock - 1, version = version + 1
WHERE id = 1 AND version = 5;   -- 0 rows updated → someone else changed it → retry
```

|             | Pessimistic               | Optimistic          |
| ----------- | ------------------------- | ------------------- |
| Best when   | High contention           | Low contention      |
| Cost        | Locks, possible deadlocks | Retries on conflict |
| Concurrency | Lower                     | Higher              |

**Rule of thumb:** optimistic for mostly-read workloads; pessimistic when conflicts are frequent and retries are expensive (e.g. flash sales).
