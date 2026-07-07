# 23. Higher-Order Components (HOC)? (Mid)

An HOC is a **function that takes a component and returns a new component** with added behavior — a pattern for reusing logic (pre-hooks era).

```tsx
function withLoading<P extends object>(Component: React.ComponentType<P>) {
  return function WithLoading({ loading, ...props }: P & { loading: boolean }) {
    if (loading) return <Spinner />;
    return <Component {...(props as P)} />;
  };
}

const UserListWithLoading = withLoading(UserList);
```

**Common real-world HOCs:** `connect()` (Redux), `withRouter`, `withTranslation`.

**Conventions:**

- **Pass through unrelated props** (`{...props}`).
- Don't mutate the input component — compose it.
- **Copy static methods** / set `displayName` for debugging (`hoistNonReactStatics`).

**Downsides that pushed the ecosystem to hooks:**

- **Wrapper hell** — deeply nested `withA(withB(withC(Comp)))` in DevTools.
- **Prop name collisions** — two HOCs injecting the same prop.
- Indirection — hard to trace where a prop comes from.

**Modern take:** **custom hooks** replace most HOCs — same logic reuse, no wrapper nesting, explicit data flow.

```tsx
// instead of withLoading, just:
const { data, loading } = useFetch(url);
if (loading) return <Spinner />;
```
