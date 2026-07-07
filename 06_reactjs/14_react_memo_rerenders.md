# 14. `React.memo` and avoiding re-renders? (Mid)

**When does a component re-render?** When its state changes, its parent re-renders, or its context value changes. A parent re-render re-renders **all children by default**, even if their props are unchanged.

**`React.memo`** skips a re-render if props are **shallowly equal** to the previous render:

```tsx
const Row = React.memo(function Row({ label }: { label: string }) {
  return <div>{label}</div>;
});
// re-renders only when `label` actually changes
```

**Shallow comparison gotcha** — new object/array/function props defeat it:

```tsx
<Row style={{ color: "red" }} /> // ❌ new object each render → memo useless
<Row onClick={() => {}} />       // ❌ new function each render
```

Fix with `useMemo` / `useCallback` for the props, or pass primitives.

**Other ways to cut re-renders:**

- **Move state down** — isolate frequently-changing state to a small leaf component.
- **Lift content up via `children`** — a parent that re-renders doesn't re-render `children` passed to it.
- **Split contexts** so unrelated consumers don't re-render.

**Custom comparator:** `React.memo(Comp, (prev, next) => prev.id === next.id)`.

**Rule:** don't `memo` everything — measure first (React DevTools Profiler). Memo adds a comparison cost that's wasteful for cheap components.
