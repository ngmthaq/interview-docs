# 26. Concurrent rendering: `useTransition` & `useDeferredValue`? (Senior)

React 18's **concurrent renderer** can interrupt, pause, and prioritize rendering so **urgent updates** (typing, clicks) aren't blocked by **expensive ones** (rendering a big filtered list).

**`useTransition`** — mark a state update as **non-urgent**. React keeps the UI responsive and can interrupt the transition for urgent input:

```tsx
const [isPending, startTransition] = useTransition();
const [query, setQuery] = useState("");
const [results, setResults] = useState<Item[]>([]);

function onChange(e: React.ChangeEvent<HTMLInputElement>) {
  setQuery(e.target.value); // urgent: input updates immediately
  startTransition(() => {
    setResults(filterHugeList(e.target.value)); // non-urgent
  });
}
// isPending → show a subtle loading state
```

**`useDeferredValue`** — derive a **lagging copy** of a value; the expensive UI reads the deferred version while the input stays snappy:

```tsx
const deferredQuery = useDeferredValue(query);
const list = useMemo(() => filterHugeList(deferredQuery), [deferredQuery]);
```

|                    | You control          | Use when                         |
| ------------------ | -------------------- | -------------------------------- |
| `useTransition`    | the **state update** | you own the setter               |
| `useDeferredValue` | a **value**          | value comes from props/elsewhere |

**Effect:** urgent updates (cursor, keystrokes) render at high priority; heavy re-renders happen in the background and can be thrown away if superseded — no janky, frozen input.
