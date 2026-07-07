# 25. `forwardRef` and `useImperativeHandle`? (Senior)

By default `ref` **cannot be passed as a prop** to a function component — it's reserved. **`forwardRef`** lets a component receive a ref and forward it to a child DOM node.

```tsx
const FancyInput = forwardRef<HTMLInputElement, { placeholder?: string }>((props, ref) => (
  <input ref={ref} {...props} />
));

// parent can now access the DOM node
const ref = useRef<HTMLInputElement>(null);
<FancyInput ref={ref} />;
ref.current?.focus();
```

**`useImperativeHandle`** customizes **what the ref exposes** — instead of the raw DOM node, expose a curated API:

```tsx
const Modal = forwardRef<{ open: () => void; close: () => void }>((_, ref) => {
  const [visible, setVisible] = useState(false);
  useImperativeHandle(ref, () => ({
    open: () => setVisible(true),
    close: () => setVisible(false),
  }));
  return visible ? <div className="modal" /> : null;
});

// parent
modalRef.current?.open();
```

**When to use:** imperative actions that don't fit the declarative model — `focus()`, `scrollTo()`, media `play()`, triggering animations, exposing `open/close`.

**Caution:** it's an **escape hatch**. Prefer props/state; reach for imperative handles only when declarative flow can't express the interaction.

**React 19 note:** `ref` is becoming a regular prop, so `forwardRef` is no longer required for new code.
