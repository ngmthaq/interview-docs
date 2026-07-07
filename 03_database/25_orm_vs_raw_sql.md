# 25. When should you use raw SQL instead of an ORM? (Senior)

An ORM is a productivity tool, not a replacement for SQL knowledge. Reach for **raw SQL / query builder** when the ORM gets in the way.

**Use raw SQL when:**

- **Complex queries** — advanced joins, window functions, CTEs, recursive queries the ORM expresses poorly.
- **Performance-critical paths** — you need full control over the exact plan and indexes used.
- **Bulk operations** — mass updates/inserts where per-entity ORM calls are too slow.
- **Reporting / analytics** — aggregations that don't map cleanly to entities.

```ts
// Drop to raw SQL for a query the ORM handles awkwardly
const rows = await prisma.$queryRaw`
  SELECT user_id, SUM(total) AS revenue
  FROM orders
  WHERE created_at >= NOW() - INTERVAL '30 days'
  GROUP BY user_id
  HAVING SUM(total) > 1000
`;
```

**Stick with the ORM for:** standard CRUD, relation loading, migrations — where it saves real time and stays safe.

**Senior takeaway:** it's not either/or. Use the ORM for the 90% of routine access, and **drop to raw SQL** (still parameterized to avoid injection) for the 10% that needs control or speed. Always know what SQL runs underneath.
