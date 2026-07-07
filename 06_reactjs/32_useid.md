# 32. What is the useId hook? (Junior)

**`useId`** generates a **stable, unique ID** that matches between server and client renders — solving hydration mismatches when you need IDs for accessibility.

```tsx
function LabeledInput({ label }: { label: string }) {
  const id = useId();
  return (
    <>
      <label htmlFor={id}>{label}</label>
      <input id={id} />
    </>
  );
}
```

**Why not `Math.random()` or a counter?**

- Random/counter IDs differ between the **server render** and **client hydration** → hydration mismatch errors.
- `useId` produces the **same value on both sides** deterministically.

**Multiple related IDs from one call** — use a prefix:

```tsx
const id = useId();
// id + "-name", id + "-email" for several fields
<input id={`${id}-email`} aria-describedby={`${id}-hint`} />;
```

**Notes:**

- It's for **IDs**, **not** for keys in lists (use stable data IDs there).
- Ideal for linking `label`/`input`, `aria-describedby`, form fields in reusable components.

**Key point:** `useId` returns an SSR-safe unique ID stable across server and client, avoiding hydration mismatches — use it for accessibility associations (`htmlFor`/`id`, `aria-*`) in reusable components, not for list keys.
