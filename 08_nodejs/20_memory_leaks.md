# 20. How do you detect and prevent memory leaks in Node.js? (Senior)

A **memory leak** is retained memory that's no longer needed — heap usage climbs until the process slows (GC pressure) or crashes (out of memory).

**Common causes:**

- **Unbounded caches / arrays** that only grow.
- **Uncleared `setInterval`** or event listeners (`emitter.on` without `off`).
- **Closures** holding large objects longer than expected.
- **Global variables** accumulating data.

```js
// LEAK — listener added per request, never removed
function handler(req, res) {
  emitter.on("event", onEvent); // grows forever
}

// FIX — remove it, or use once / AbortSignal
function handler(req, res) {
  emitter.once("event", onEvent);
}
```

**Detection tools:**

- `process.memoryUsage()` — watch `heapUsed` trend over time.
- **Heap snapshots** in Chrome DevTools (`node --inspect`) — compare snapshots to find growing object counts.
- `--max-old-space-size` to cap heap; clinic.js / heapdump for profiling.

**Prevention:** bound caches (LRU with TTL), always clear timers/listeners, avoid unnecessary globals, and load-test while monitoring memory.

**Key point:** leaks come from references that outlive their usefulness (caches, listeners, timers, globals); detect them by trending `heapUsed` and comparing heap snapshots, and prevent them by bounding growth and cleaning up subscriptions.
