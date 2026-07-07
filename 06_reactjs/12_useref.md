# 12. `useRef` — what is it for? (Mid)

`useRef` returns a **mutable container** (`{ current }`) that **persists across renders** and does **not** trigger a re-render when changed.

**Two main uses:**

**1. Accessing DOM elements:**

```tsx
function TextInput() {
  const inputRef = useRef<HTMLInputElement>(null);
  useEffect(() => inputRef.current?.focus(), []); // focus on mount
  return <input ref={inputRef} />;
}
```

**2. Holding mutable values that shouldn't cause re-renders** — timers, previous values, instance-like data:

```tsx
const timerRef = useRef<number>();
timerRef.current = window.setInterval(tick, 1000);
```

**`useRef` vs `useState`:**

|                 | `useState`       | `useRef`      |
| --------------- | ---------------- | ------------- |
| Triggers render | ✅ on change     | ❌ never      |
| Persists        | ✅               | ✅            |
| Read timing     | value per render | always latest |

**Key distinction:** changing `ref.current` is **synchronous and silent** — the UI won't update. Use state for anything the UI displays; use a ref for values you need to remember but not render.

**Gotcha:** don't read/write `ref.current` **during render** (it's a side effect and breaks purity) — do it in effects or event handlers.
