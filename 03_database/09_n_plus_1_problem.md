# 9. What is the N+1 query problem? (Mid)

The **N+1 problem** happens when code runs **1 query to fetch a list**, then **N more queries** (one per item) to fetch related data — flooding the DB.

```ts
// ❌ N+1: 1 query for users, then 1 query PER user for orders
const users = await db.query("SELECT * FROM users"); // 1
for (const u of users) {
  u.orders = await db.query(
    // N
    "SELECT * FROM orders WHERE user_id = $1",
    [u.id],
  );
}
```

**Fixes:**

```ts
// ✅ 1. Eager load with a JOIN
db.query(`SELECT * FROM users u LEFT JOIN orders o ON o.user_id = u.id`);

// ✅ 2. Batch with WHERE IN (2 queries total)
const ids = users.map((u) => u.id);
db.query("SELECT * FROM orders WHERE user_id = ANY($1)", [ids]);
```

**In ORMs:** use eager loading (`include`, `join`, `with`, `select_related`) instead of lazy per-item access. It's one of the most common real-world performance bugs.
