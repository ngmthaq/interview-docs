# 14. What is denormalization and when is it useful? (Mid)

**Denormalization** deliberately **adds redundant data** to avoid expensive joins and speed up reads — the opposite of normalization.

```sql
-- Normalized: must JOIN to show order with customer name
orders(id, customer_id, total)

-- Denormalized: store the name directly on the order
orders(id, customer_id, customer_name, total) -- no join needed to display
```

**When it helps:**

- **Read-heavy** systems where joins are a bottleneck.
- Precomputed aggregates (e.g. `post.comment_count`) to avoid `COUNT(*)` on every load.
- Reporting / analytics tables.

**Trade-offs:**

- **Data can get out of sync** — you must update every copy on change.
- More storage; write complexity increases.

**Key point:** normalize by default for integrity; denormalize **selectively** for measured read performance. Often paired with triggers or app logic to keep copies consistent.
