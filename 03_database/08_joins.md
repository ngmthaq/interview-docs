# 8. Explain the types of JOINs. (Junior)

A **JOIN** combines rows from two tables based on a related column.

| JOIN           | Returns                                        |
| -------------- | ---------------------------------------------- |
| **INNER**      | Only rows with a match in **both** tables      |
| **LEFT**       | All left rows + matching right (nulls if none) |
| **RIGHT**      | All right rows + matching left                 |
| **FULL OUTER** | All rows from both, matched where possible     |
| **CROSS**      | Cartesian product (every combination)          |

```sql
-- Users and their orders (users without orders excluded)
SELECT u.name, o.total
FROM users u
INNER JOIN orders o ON o.user_id = u.id;

-- All users, even those with no orders
SELECT u.name, o.total
FROM users u
LEFT JOIN orders o ON o.user_id = u.id; -- o.total is NULL if no order
```

**Interview tip:** the classic question is "INNER vs LEFT JOIN" — INNER drops non-matching rows; LEFT keeps all left-side rows and fills missing right-side columns with `NULL`.
