# 29. State management options — when to use what? (Senior)

Not all state is the same. Pick the tool by **scope** and **kind** of state.

**Categories of state:**

- **Local UI** — toggles, inputs → `useState` / `useReducer`.
- **Shared/global client** — auth, theme, cart → Context or a store.
- **Server/remote** — API data → a data-fetching library (cache, not "state").
- **URL** — filters, pagination → the router / query params.

**Client state libraries:**

| Tool              | Model                            | Best for                                 |
| ----------------- | -------------------------------- | ---------------------------------------- |
| **Context**       | built-in, prop-drill fix         | low-frequency global (theme/auth)        |
| **Redux Toolkit** | single store, reducers, devtools | large apps, complex flows, traceability  |
| **Zustand**       | small hook-based store           | simple global state, minimal boilerplate |
| **Jotai/Recoil**  | atomic state                     | fine-grained, derived atoms              |

**Server state — treat it separately:**

**React Query (TanStack)** / **SWR** / **RTK Query** handle caching, deduping, background refetch, and stale-while-revalidate — things a client store does poorly:

```tsx
const { data, isLoading } = useQuery({
  queryKey: ["user", id],
  queryFn: () => fetchUser(id),
});
```

**Key insight:** most "global state" is actually **server cache**. Don't put fetched data in Redux — use a query library. Reserve client stores for genuine client-only shared state.

**Rule:** start with local state → lift up → Context → reach for a library only when complexity demands it. Avoid premature Redux.
