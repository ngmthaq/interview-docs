# 6. What is an index and why use one? (Junior → Mid)

An **index** is a data structure (usually a **B-tree**) that lets the DB find rows **without scanning the whole table** — like a book's index.

```sql
-- Without index: full table scan, O(n)
SELECT * FROM users WHERE email = 'a@b.com';

-- Create an index → lookup becomes ~O(log n)
CREATE INDEX idx_users_email ON users(email);
```

**Benefits:**

- Dramatically faster reads on filtered/sorted columns (`WHERE`, `JOIN`, `ORDER BY`).

**Costs (the trade-off):**

- **Slower writes** — every INSERT/UPDATE must also update the index.
- **Extra storage.**

**Rule of thumb:** index columns you frequently filter or join on; don't index everything. High-selectivity columns (many distinct values, like email) benefit most.
