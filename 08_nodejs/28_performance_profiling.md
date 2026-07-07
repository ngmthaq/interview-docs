# 28. How do you profile and optimize Node.js performance? (Senior)

Optimization starts with **measurement**, not guessing.

**Profiling tools:**

- **`node --inspect`** + Chrome DevTools — CPU profiles, flame graphs, heap snapshots.
- **`node --prof`** — V8 sampling profiler; analyze with `--prof-process`.
- **`clinic.js`** (Doctor/Flame/Bubbleprof) — diagnoses event-loop delay, CPU, and async bottlenecks.
- **`perf_hooks`** — measure specific code paths in-process.

```ts
import { performance } from "perf_hooks";

const start = performance.now();
await expensiveOperation();
console.log(`Took ${(performance.now() - start).toFixed(1)}ms`);
```

**Common optimizations:**

- **Don't block the event loop** — offload CPU work to workers; watch **event-loop lag**.
- **Cache** expensive results (in-memory LRU, Redis).
- **Stream** large payloads instead of buffering.
- Use **connection pooling** for DBs; batch queries; avoid N+1.
- Enable **HTTP keep-alive** and compression (`gzip`/`brotli`).
- Scale horizontally with **cluster/PM2** across cores.

**Key point:** profile first (`--inspect`, clinic.js, `perf_hooks`) to find the real bottleneck; typical wins are keeping the event loop unblocked, caching, streaming, pooling DB connections, and scaling across cores — never optimize blind.
