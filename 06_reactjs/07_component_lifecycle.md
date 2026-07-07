# 7. Component lifecycle (hooks vs class)? (Mid)

Three phases: **mount → update → unmount**. Hooks express all of them via `useEffect`.

| Phase   | Class method           | Hook equivalent                       |
| ------- | ---------------------- | ------------------------------------- |
| Mount   | `componentDidMount`    | `useEffect(fn, [])`                   |
| Update  | `componentDidUpdate`   | `useEffect(fn, [deps])`               |
| Unmount | `componentWillUnmount` | cleanup return in `useEffect(fn, [])` |

```tsx
useEffect(() => {
  console.log("mounted"); // componentDidMount
  return () => console.log("unmounted"); // componentWillUnmount
}, []);

useEffect(() => {
  console.log("id changed"); // componentDidUpdate (on id)
}, [id]);
```

**Render vs commit:**

- **Render phase** — React calls your component to compute the JSX. Must be **pure** (no side effects).
- **Commit phase** — React applies changes to the DOM, then runs effects.

**`useLayoutEffect`** — like `useEffect` but fires **synchronously after DOM mutations, before paint**. Use only when you must measure/adjust layout to avoid a visible flicker; otherwise prefer `useEffect`.

**Mental model:** a class had many named methods; hooks collapse them into effects grouped **by concern**, not by lifecycle timing — related setup and cleanup live together.
