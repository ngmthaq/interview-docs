# 20. How do you diagnose and optimize a slow query? (Senior)

**Step 1 — measure with `EXPLAIN ANALYZE`.** It shows the query plan and where time goes.

```sql
EXPLAIN ANALYZE
SELECT * FROM orders WHERE user_id = 42;
```

Look for red flags:

- **Seq Scan** on a large table where an index should apply.
- High **rows** estimates vs actual (bad statistics).
- Expensive **sorts** or **nested loop** joins on big sets.

**Step 2 — common fixes:**

- **Add/adjust an index** on filtered/joined columns (respecting leftmost-prefix).
- **Select only needed columns** — avoid `SELECT *`.
- **Fix N+1** — batch or join instead of per-row queries.
- **Rewrite** — sargable predicates (avoid functions on indexed columns: `WHERE date(col)=...` breaks index use).
- **Paginate** with keyset pagination instead of large `OFFSET`.
- Update **table statistics** (`ANALYZE`) so the planner chooses well.

**Step 3 — verify** by re-running `EXPLAIN ANALYZE` and comparing actual time.

**Senior mindset:** optimize based on **evidence** (the plan and real metrics), not guesses. Also consider caching, denormalization, or read replicas when query tuning isn't enough.
