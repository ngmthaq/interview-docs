# 30. What caching strategies do you use in Node.js? (Senior)

Caching stores expensive results to serve them faster and reduce load on databases/APIs.

**Levels of caching:**

- **In-memory** — fastest, per-process. Use a bounded LRU (`lru-cache`), not a raw object (which leaks).
- **Distributed** — **Redis/Memcached**, shared across instances; survives restarts and works with clustering.
- **HTTP** — `Cache-Control`, `ETag`, CDN caching for responses.

```ts
import { LRUCache } from "lru-cache";

const cache = new LRUCache<string, User>({ max: 1000, ttl: 60_000 }); // 1 min

async function getUser(id: string): Promise<User> {
  const cached = cache.get(id);
  if (cached) return cached; // cache hit

  const user = await db.users.findById(id); // cache miss
  cache.set(id, user);
  return user;
}
```

**Key concerns:**

- **Invalidation** — the hard part; use **TTLs**, or explicitly evict on writes (write-through / cache-aside).
- **In-memory limits** — bound size (LRU) or you leak memory; it's also **per-process**, so instances can diverge.
- **Stampede protection** — coalesce concurrent misses so one DB call serves many waiters.

**Key point:** cache with bounded in-memory LRUs for hot per-process data and Redis for shared/distributed caching; the real challenge is **invalidation** — lean on TTLs and cache-aside eviction, and always bound in-memory caches to avoid leaks.
