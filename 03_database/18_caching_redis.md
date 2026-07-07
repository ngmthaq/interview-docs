# 18. How does caching (e.g. Redis) help databases? (Mid → Senior)

A **cache** stores frequently accessed data in fast memory (like **Redis**) to avoid hitting the slower database repeatedly.

```ts
async function getUser(id: number) {
  const cached = await redis.get(`user:${id}`);
  if (cached) return JSON.parse(cached); // cache hit — fast

  const user = await db.query("SELECT * FROM users WHERE id=$1", [id]); // miss
  await redis.set(`user:${id}`, JSON.stringify(user), "EX", 300); // TTL 5min
  return user;
}
```

**Cache-aside** (above) is the most common strategy: app checks cache, falls back to DB, then populates cache.

**Key concerns:**

- **Invalidation** — update/delete cache when the underlying data changes (the hard part).
- **TTL** — expire entries to bound staleness.
- **Stampede** — many misses at once hammer the DB; mitigate with locks or staggered TTLs.

**Benefits:** massive read latency reduction and DB load relief. **Trade-off:** possible **stale data** and added complexity.
