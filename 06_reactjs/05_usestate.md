# 5. `useState` — how does it work? (Fresher)

`useState` adds local state to a function component. It returns a **[value, setter]** pair.

```tsx
const [count, setCount] = useState(0);
setCount(count + 1); // schedule re-render with new value
```

**Updates are asynchronous & batched** — reading `count` right after `setCount` gives the old value:

```tsx
setCount(count + 1);
setCount(count + 1);
console.log(count); // still old — updates apply on next render
```

**Functional updates** — use the updater form when the new value depends on the previous one:

```tsx
setCount((c) => c + 1);
setCount((c) => c + 1); // now both apply → +2
```

**State is immutable** — replace, don't mutate:

```tsx
setUser({ ...user, name: "New" }); // ✅ new object
user.name = "New"; // ❌ won't re-render
setItems([...items, newItem]); // ✅ new array
```

**Lazy initialization** — pass a function for expensive initial state (runs once):

```tsx
const [data] = useState(() => expensiveCompute());
```

**Key idea:** calling the setter with a **new reference** is what tells React to re-render. Mutating in place is invisible to React.
