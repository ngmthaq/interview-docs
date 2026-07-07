# 6. `useEffect` — how does it work? (Mid)

`useEffect` runs **side effects** (data fetching, subscriptions, DOM, timers) **after render**.

```tsx
useEffect(() => {
  // effect runs after paint
  const id = setInterval(tick, 1000);
  return () => clearInterval(id); // cleanup
}, [dep]); // dependency array
```

**The dependency array controls when it runs:**

| Deps      | Runs                                     |
| --------- | ---------------------------------------- |
| _omitted_ | after **every** render                   |
| `[]`      | **once** on mount (+ cleanup on unmount) |
| `[a, b]`  | on mount and whenever `a` or `b` changes |

**Cleanup** runs before the next effect and on unmount — use it to unsubscribe, clear timers, abort fetches:

```tsx
useEffect(() => {
  const ctrl = new AbortController();
  fetch(url, { signal: ctrl.signal }).then(/* ... */);
  return () => ctrl.abort();
}, [url]);
```

**Common pitfalls:**

- **Missing deps** → stale closures. Include every value the effect reads (the `exhaustive-deps` lint rule enforces this).
- **Objects/functions as deps** change identity every render → wrap in `useMemo`/`useCallback`.
- **Don't use effects for derived state** — compute it during render instead.

**React 18 note:** in Strict Mode (dev), effects run **twice** on mount to surface missing cleanup.
