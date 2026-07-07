# 16. Rules of Hooks? (Mid)

Two rules make hooks work reliably:

**1. Only call hooks at the top level** — never inside conditions, loops, or nested functions:

```tsx
// ❌ conditional hook
if (isLoggedIn) {
  const [x] = useState(0);
}

// ✅ always called, condition inside
const [x, setX] = useState(0);
if (isLoggedIn) {
  /* use x */
}
```

**2. Only call hooks from React functions** — components or other custom hooks, not plain JS functions.

**Why the order matters:** React tracks hook state by **call order**, not by name. It's essentially an array indexed by call position:

```
render 1: useState → slot 0, useEffect → slot 1
render 2: useState → slot 0, useEffect → slot 1  ✅ consistent
```

If a hook is conditionally skipped, the slots shift and React associates state with the **wrong** hook → bugs or crashes.

**Enforcement:** the `eslint-plugin-react-hooks` plugin catches violations at lint time (`rules-of-hooks` + `exhaustive-deps`).

**Practical takeaways:**

- Put early `return`s **after** all hook calls.
- To conditionally run logic, put the condition **inside** the hook (e.g. `useEffect(() => { if (x) … }, [x])`), not around the hook call.
