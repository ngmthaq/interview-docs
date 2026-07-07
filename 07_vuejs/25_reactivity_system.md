# 25. How does Vue's reactivity system work? (Senior)

Vue 3 tracks state changes with **ES6 Proxies**. When you create reactive state, Vue wraps it in a Proxy that **intercepts get and set** operations.

**The mechanism — track & trigger:**

1. **Track (on get)** — when a reactive property is read _during_ an effect (a render, computed, or watcher), Vue records that this effect **depends on** that property.
2. **Trigger (on set)** — when the property is written, Vue re-runs all effects that depend on it.

```ts
// simplified concept
const obj = new Proxy(target, {
  get(t, key) {
    track(t, key); // remember who's reading
    return t[key];
  },
  set(t, key, val) {
    t[key] = val;
    trigger(t, key); // re-run dependents
    return true;
  },
});
```

**Vue 2 vs Vue 3:**

|                    | Vue 2                           | Vue 3                  |
| ------------------ | ------------------------------- | ---------------------- |
| Mechanism          | `Object.defineProperty`         | `Proxy`                |
| New props          | not detected (needed `Vue.set`) | detected automatically |
| Array index/length | not tracked                     | tracked                |
| Deletions          | not detected                    | detected               |

Proxies fixed Vue 2's well-known limitations (adding/removing properties, array index assignment).

**`ref` vs `reactive` internally:** `reactive` proxies an object; `ref` uses a `{ value }` object with getter/setter accessors (so primitives can be reactive too).

**Practical implications:**

- **Destructuring** a `reactive` object breaks tracking — the extracted value is a plain primitive. Use `toRefs`.
- Reactivity is **lazy and dependency-precise** — only effects that actually read a value re-run when it changes.
- `shallowRef` / `shallowReactive` opt out of deep tracking for performance with large structures.
