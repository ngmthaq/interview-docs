# 25. How does garbage collection work, and what causes memory leaks? (Senior)

**Garbage collection (GC):** JS automatically frees memory for objects that are **no longer reachable** from the root (global, call stack). The main algorithm is **mark-and-sweep** — mark everything reachable, sweep the rest.

**A memory leak = objects that stay reachable but are no longer needed**, so GC can't reclaim them.

**Common causes:**

```js
// 1. Forgotten timers/intervals
setInterval(() => doWork(bigData), 1000); // never cleared → bigData retained

// 2. Detached DOM references
const cache = {};
cache.el = document.getElementById("node");
document.body.removeChild(cache.el); // removed from DOM but still referenced

// 3. Growing global/module data structures
const seen = [];
function track(item) {
  seen.push(item);
} // never cleaned up

// 4. Closures holding large scopes
function outer() {
  const huge = new Array(1e6);
  return () => huge[0]; // keeps `huge` alive as long as the closure lives
}

// 5. Unremoved event listeners
el.addEventListener("click", handler); // must removeEventListener when done
```

**Prevention:**

- Clear timers (`clearInterval`), remove listeners, null out references.
- Use **`WeakMap`/`WeakSet`** for caches keyed by objects (don't prevent GC).
- Profile with Chrome DevTools **Memory / heap snapshots** to find retained objects.

**Key point:** GC is automatic, but leaks happen when you **unintentionally keep references alive** — timers, listeners, closures, and global collections are the usual suspects.
