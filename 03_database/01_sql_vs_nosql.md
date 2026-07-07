# 1. SQL vs NoSQL — what's the difference? (Fresher)

|               | SQL (Relational)             | NoSQL (Non-relational)                             |
| ------------- | ---------------------------- | -------------------------------------------------- |
| Structure     | Tables with fixed **schema** | Flexible: documents, key-value, graph, wide-column |
| Relationships | Joins, foreign keys          | Usually embedded / denormalized                    |
| Scaling       | Vertical (bigger server)     | Horizontal (add nodes)                             |
| Consistency   | Strong (ACID)                | Often eventual (BASE)                              |
| Examples      | PostgreSQL, MySQL            | MongoDB, Redis, Cassandra                          |

```sql
-- SQL: structured, related tables
SELECT u.name, o.total
FROM users u
JOIN orders o ON o.user_id = u.id;
```

**When to choose:**

- **SQL** — structured data, complex queries, transactions (banking, orders).
- **NoSQL** — flexible/changing schema, huge scale, simple access patterns (caching, logs, real-time feeds).

**Key point:** it's not "better vs worse" — pick based on data shape and access patterns.
