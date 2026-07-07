# 13. `useMemo` vs `useCallback`? (Mid)

Both **memoize** across renders to avoid recomputing/recreating. Difference is **what** they cache.

- **`useMemo`** — caches a **computed value**.
- **`useCallback`** — caches a **function reference**.

```tsx
const sorted = useMemo(() => list.sort(cmp), [list]); // caches result
const onClick = useCallback(() => doThing(id), [id]); // caches function
```

In fact `useCallback(fn, deps)` ≡ `useMemo(() => fn, deps)`.

**Why cache a function?** Referential stability. A new function every render breaks:

- `React.memo` children (new prop reference → they re-render).
- `useEffect` deps (effect re-runs every render).

```tsx
const Child = React.memo(ChildImpl);
// without useCallback, onAction is new each render → Child always re-renders
<Child onAction={useCallback(() => {}, [])} />;
```

**When to use:**

- Expensive computations (`useMemo`).
- Passing callbacks/values to memoized children or effect deps (`useCallback`/`useMemo`).

**When NOT to:** memoization has a cost (memory + dep comparison). For cheap calculations it's premature optimization — don't wrap everything.

**React 19 note:** the React Compiler auto-memoizes, reducing the need to write these by hand.
