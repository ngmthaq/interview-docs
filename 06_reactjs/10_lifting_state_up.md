# 10. Lifting state up? (Mid)

When two components need to share or stay in sync with the same data, move that state to their **closest common parent** and pass it down as props. This keeps a **single source of truth**.

```tsx
function Parent() {
  const [query, setQuery] = useState(""); // shared state lives here

  return (
    <>
      <SearchBox query={query} onChange={setQuery} />
      <Results query={query} /> {/* reads the same state */}
    </>
  );
}

function SearchBox({ query, onChange }: Props) {
  return <input value={query} onChange={(e) => onChange(e.target.value)} />;
}
```

**Pattern:** state lives in the parent; children receive the **value** (down) and a **callback** to update it (up).

**Why:** avoids two components holding divergent copies of the same data that drift out of sync.

**Trade-off — prop drilling:** passing props through many intermediate layers gets tedious. Solutions:

- **Context** — for widely-shared data (theme, auth, locale).
- **State libraries** — Redux, Zustand, Jotai for complex global state.
- **Component composition** — pass JSX via `children` to avoid threading props.

**Rule:** lift state only as high as needed — keep it as **local as possible**, share it as high as **necessary**.
