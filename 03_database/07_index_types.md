# 7. What types of indexes exist? (Mid)

| Index type           | Best for                                                     |
| -------------------- | ------------------------------------------------------------ |
| **B-tree** (default) | Equality & range queries (`=`, `<`, `>`, `BETWEEN`, sorting) |
| **Hash**             | Exact-match equality only                                    |
| **Composite**        | Queries filtering on multiple columns together               |
| **Unique**           | Enforce uniqueness + speed up lookups                        |
| **Partial**          | Index only a subset of rows (`WHERE active = true`)          |
| **Full-text**        | Searching text content                                       |

**Composite index — column order matters:**

```sql
CREATE INDEX idx_orders ON orders(user_id, created_at);

-- ✅ uses index (leftmost prefix)
SELECT * FROM orders WHERE user_id = 1 AND created_at > '2024-01-01';
-- ✅ uses index
SELECT * FROM orders WHERE user_id = 1;
-- ❌ can't use index efficiently (skips leftmost column)
SELECT * FROM orders WHERE created_at > '2024-01-01';
```

**Key point:** a composite index follows the **leftmost-prefix rule** — order columns by how you query them (equality columns first, range last).
