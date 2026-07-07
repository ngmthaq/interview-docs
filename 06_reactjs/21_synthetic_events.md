# 21. Synthetic events? (Mid)

React wraps native DOM events in a **`SyntheticEvent`** — a cross-browser wrapper with the same API everywhere (`e.target`, `e.preventDefault()`, `e.stopPropagation()`).

```tsx
function Form() {
  const onSubmit = (e: React.FormEvent) => {
    e.preventDefault(); // works identically across browsers
    console.log(e.currentTarget);
  };
  return <form onSubmit={onSubmit} />;
}
```

**Event delegation:** React does **not** attach a listener to every node. It attaches **one listener at the root** (the app container in React 17+; `document` before that) and dispatches events through its own tree. Cheaper and consistent.

**`e.target` vs `e.currentTarget`:**

- `target` — the element that fired the event.
- `currentTarget` — the element the handler is attached to.

**Key points:**

- Handlers are **camelCase**: `onClick`, `onChange`, `onKeyDown`.
- Pass a **function reference**, not a call: `onClick={handle}` not `onClick={handle()}`.
- To stop default browser behavior use `e.preventDefault()` (returning `false` does nothing in React).

**Note:** since React 17, event pooling was **removed** — you can safely access the event asynchronously without calling `e.persist()`.
