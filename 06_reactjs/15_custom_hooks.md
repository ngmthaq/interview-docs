# 15. Custom hooks? (Mid)

A custom hook is a **function starting with `use`** that calls other hooks to **extract and reuse stateful logic** between components.

```tsx
function useToggle(initial = false) {
  const [on, setOn] = useState(initial);
  const toggle = useCallback(() => setOn((o) => !o), []);
  return [on, toggle] as const;
}

// usage
const [isOpen, toggleOpen] = useToggle();
```

**A realistic example** — data fetching:

```tsx
function useFetch<T>(url: string) {
  const [data, setData] = useState<T | null>(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    let active = true;
    fetch(url)
      .then((r) => r.json())
      .then((d) => active && setData(d))
      .finally(() => active && setLoading(false));
    return () => {
      active = false;
    };
  }, [url]);

  return { data, loading };
}
```

**Key points:**

- Must start with **`use`** so React's lint rules apply.
- **Each call gets its own isolated state** — two components using `useToggle` don't share state.
- They compose logic, **not markup** (that's what components are for).

**Why:** replaces class-era HOCs and render props for logic reuse — flatter, no wrapper hell.
