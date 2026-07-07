# 4. Props vs state? (Fresher)

|                 | Props                        | State                       |
| --------------- | ---------------------------- | --------------------------- |
| Owned by        | parent (passed in)           | the component itself        |
| Mutable         | ❌ read-only inside child    | ✅ via setter               |
| Purpose         | configure / pass data down   | data that changes over time |
| Triggers render | when parent passes new value | when updated via setter     |

```tsx
function Child({ label }: { label: string }) {
  const [open, setOpen] = useState(false); // state: internal
  return <button onClick={() => setOpen(!open)}>{label}</button>; // prop: from parent
}

<Child label="Toggle" />; // parent supplies prop
```

**Props flow down (one-way data flow):** a parent passes data to children; children cannot mutate props. To send data **up**, the parent passes a **callback**:

```tsx
function Parent() {
  const [val, setVal] = useState("");
  return <Input onChange={setVal} />; // child calls onChange to notify parent
}
```

**Rules:**

- **Never mutate props** — treat them as read-only.
- **Never mutate state directly** — always use the setter (`setState`/`setX`) so React knows to re-render.

**Mental model:** props are function arguments; state is the component's memory between renders.
