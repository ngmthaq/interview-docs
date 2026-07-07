# 2. What is JSX? (Fresher)

JSX is a **syntax extension** that lets you write HTML-like markup in JavaScript. It is **not** HTML and not a string — it compiles to function calls.

```tsx
const el = <h1 className="title">Hi</h1>;
// compiles to:
const el2 = React.createElement("h1", { className: "title" }, "Hi");
```

**Key rules:**

- Use `className` (not `class`) and `htmlFor` (not `for`) — reserved JS words.
- **Embed expressions** with `{}`: `<p>{user.name}</p>`.
- Must return **one root element** — wrap siblings in a `<Fragment>` / `<>…</>`.
- Attributes are **camelCase**: `onClick`, `tabIndex`.
- Self-close tags: `<img />`, `<br />`.

```tsx
function List({ items }: { items: string[] }) {
  return (
    <>
      {items.map((it) => (
        <li key={it}>{it}</li>
      ))}
    </>
  );
}
```

**Conditional rendering** uses plain JS:

```tsx
{
  isLoggedIn ? <Dashboard /> : <Login />;
}
{
  hasError && <Error />;
}
```

**Note:** JSX is optional sugar — everything compiles down to `React.createElement` (or the automatic runtime `jsx()` in modern setups).
