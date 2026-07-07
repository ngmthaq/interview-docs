# 15. Partitioning vs Sharding? (Senior)

Both split large tables, but at different levels.

- **Partitioning** — split one table into pieces **within the same database/server** (by range, list, or hash). Transparent to queries.
- **Sharding** — split data **across multiple servers/nodes**. Each shard is an independent database.

```sql
-- Partitioning (Postgres): one logical table, many physical partitions
CREATE TABLE logs (id BIGINT, created_at DATE)
PARTITION BY RANGE (created_at);

CREATE TABLE logs_2024 PARTITION OF logs
  FOR VALUES FROM ('2024-01-01') TO ('2025-01-01');
```

```
Sharding: users A–M → DB node 1,  users N–Z → DB node 2
```

|            | Partitioning                   | Sharding                            |
| ---------- | ------------------------------ | ----------------------------------- |
| Scope      | Single server                  | Multiple servers                    |
| Goal       | Manage big tables, prune scans | Scale beyond one machine            |
| Complexity | Lower                          | Higher (routing, cross-shard joins) |

**Key point:** partition first (simpler); shard when a single server can't hold the data or load. Choosing a good **shard key** is the hard part.
