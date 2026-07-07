# 22. Fragments and Portals? (Mid)

**Fragment** — groups children **without adding an extra DOM node**. Solves "components must return one root" without wrapper `<div>` clutter.

```tsx
function Row() {
  return (
    <>
      <td>A</td>
      <td>B</td>
    </>
  );
}
```

Use the long form `<React.Fragment key={id}>` when you need a **key** (e.g. in a list). Fragments matter for valid HTML — a `<table>` can't have a `<div>` between `<tr>` and `<td>`.

**Portal** — renders children into a **different part of the DOM tree**, outside the parent's hierarchy, while keeping React context and events intact.

```tsx
function Modal({ children }: { children: React.ReactNode }) {
  return createPortal(
    <div className="overlay">{children}</div>,
    document.body, // rendered here, not inside the parent
  );
}
```

**Why portals:** escape `overflow: hidden` / `z-index` stacking contexts for **modals, tooltips, dropdowns, toasts**.

**Key behavior:** even though the DOM node lives elsewhere, the portal is still a **React child** of its parent — so:

- Context flows through normally.
- **Events bubble through the React tree**, not the DOM tree — a click inside the portal bubbles to its React parent, not to `document.body`'s ancestors.
