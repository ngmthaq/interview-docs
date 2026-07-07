# 9. Controlled vs uncontrolled components? (Mid)

For form inputs, the question is **who owns the value** — React state or the DOM.

**Controlled** — React state is the single source of truth; value flows in via `value`, changes flow out via `onChange`:

```tsx
function Form() {
  const [name, setName] = useState("");
  return <input value={name} onChange={(e) => setName(e.target.value)} />;
}
```

**Uncontrolled** — the DOM keeps the value; you read it via a ref when needed:

```tsx
function Form() {
  const ref = useRef<HTMLInputElement>(null);
  const submit = () => console.log(ref.current?.value);
  return <input ref={ref} defaultValue="" />;
}
```

|                 | Controlled               | Uncontrolled       |
| --------------- | ------------------------ | ------------------ |
| Source of truth | React state              | DOM                |
| Value access    | from state               | via `ref`          |
| Validation      | easy, on every keystroke | on submit / manual |
| Re-renders      | on each keystroke        | none               |

**When to use each:**

- **Controlled** (default) — live validation, conditional UI, formatting as you type.
- **Uncontrolled** — simple forms, file inputs (`<input type="file">` is always uncontrolled), or integrating non-React code.

**Rule:** prefer controlled for predictability; reach for uncontrolled to avoid re-renders on large/simple forms.
