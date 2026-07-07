# 33. What are WeakMap and WeakSet? (Senior)

**`WeakMap`** and **`WeakSet`** hold **weak references** to objects — if nothing else references a key/value, it can be **garbage collected**. This prevents memory leaks in caching and metadata scenarios.

```js
const cache = new WeakMap();

function getData(obj) {
  if (cache.has(obj)) return cache.get(obj); // cached
  const result = expensiveComputation(obj);
  cache.set(obj, result);
  return result;
}
// When `obj` is no longer referenced anywhere, its cache entry is auto-collected.
```

**Key differences from Map/Set:**

- **Keys must be objects** (not primitives).
- **Not iterable** — no `.size`, `.keys()`, `.forEach()`, or clearing. (Because entries can vanish at any time, enumeration wouldn't be deterministic.)
- Entries **don't prevent** garbage collection of their keys.

**Use cases:**

- **Caching/memoization** keyed by object without leaking memory.
- **Private data** associated with an instance.
- Tracking objects (e.g. "have I seen this node?") without keeping them alive.

**Key point:** `WeakMap`/`WeakSet` store object keys weakly so entries are garbage-collected when the key is otherwise unreferenced — ideal for leak-free caches and per-object metadata; the trade-off is object-only keys and no enumeration/`size`.
