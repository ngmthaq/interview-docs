# 19. How do you optimize Express performance? (Senior)

Express itself is thin; most gains come from **how you use Node and I/O**.

```ts
import compression from "compression";
app.use(compression()); // gzip/brotli responses
```

**Techniques:**

- **Compression** — `compression` middleware shrinks response payloads.
- **Caching** — cache expensive results (Redis/in-memory LRU); set HTTP `Cache-Control`/`ETag`.
- **Don't block the event loop** — offload CPU work to `worker_threads`; keep handlers async.
- **DB efficiency** — connection pooling, indexes, avoid N+1, paginate large results.
- **Cluster / PM2** — run one process per core to use all CPUs.
- **Reverse proxy** — let nginx handle TLS, static files, and load balancing.
- **Keep-alive** connections and HTTP/2 at the proxy.
- **Limit middleware** — every global middleware runs per request; remove unused ones.

**Measure first:** profile with `clinic.js` / `--inspect` and watch event-loop lag before optimizing.

**Key point:** speed up Express by compressing responses, caching, keeping the event loop unblocked, tuning DB access, and scaling across cores with cluster/PM2 behind a reverse proxy — but profile to find the real bottleneck first.
