# 33. What is useDeferredValue? (Mid)

**`useDeferredValue`** lets you **defer** re-rendering an expensive part of the UI, keeping the app responsive during rapid updates (like typing in a search box). It's a concurrent-React feature.

```tsx
function Search() {
  const [query, setQuery] = useState("");
  const deferredQuery = useDeferredValue(query); // lags behind during bursts

  return (
    <>
      <input value={query} onChange={(e) => setQuery(e.target.value)} />
      {/* Expensive list uses the deferred value — stays responsive */}
      <SlowResults query={deferredQuery} />
    </>
  );
}
```

**How it works:**

- The input updates **immediately** (`query`), keeping typing snappy.
- `deferredQuery` updates at a **lower priority** — React may show a slightly stale list while catching up, then re-renders with the latest.
- Wrap the expensive child in `React.memo` so it only re-renders when the deferred value changes.

**`useDeferredValue` vs `useTransition`:**

- `useTransition` marks a **state update** as non-urgent (you control the setter).
- `useDeferredValue` defers a **value** you receive (e.g. a prop) without owning the update.

**Key point:** `useDeferredValue` produces a lower-priority "lagging" copy of a value so expensive renders don't block urgent updates like typing — pair with `React.memo`; use it when you have a value to defer, and `useTransition` when you own the state update.
