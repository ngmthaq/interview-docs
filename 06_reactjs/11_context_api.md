# 11. Context API? (Mid)

Context passes data through the tree **without prop drilling** — any descendant can read it directly.

```tsx
const ThemeContext = createContext<"light" | "dark">("light");

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Button() {
  const theme = useContext(ThemeContext); // reads nearest Provider
  return <button className={theme}>Click</button>;
}
```

**Good for:** low-frequency global data — theme, current user/auth, locale, feature flags.

**The re-render caveat:** **every consumer re-renders when the Provider's `value` changes**. Passing a fresh object each render triggers all consumers:

```tsx
<Ctx.Provider value={{ user, setUser }}> // ❌ new object every render
<Ctx.Provider value={useMemo(() => ({ user, setUser }), [user])}> // ✅ memoized
```

**Mitigations:**

- Memoize the `value`.
- **Split contexts** — separate rarely-changing data from frequently-changing data.
- For high-frequency global state (many updates), prefer a state library (Redux/Zustand) with selector-based subscriptions.

**Rule:** Context solves **prop drilling**, not general state management. It's a transport, not a store.
