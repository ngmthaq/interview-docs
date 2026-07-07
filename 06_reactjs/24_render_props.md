# 24. Render props? (Mid)

A **render prop** is a prop whose value is a **function that returns JSX** — the component calls it to let the consumer decide what to render, sharing state/logic without dictating markup.

```tsx
function MouseTracker({ render }: { render: (pos: { x: number; y: number }) => React.ReactNode }) {
  const [pos, setPos] = useState({ x: 0, y: 0 });
  return (
    <div onMouseMove={(e) => setPos({ x: e.clientX, y: e.clientY })}>
      {render(pos)} {/* consumer controls output */}
    </div>
  );
}

// usage
<MouseTracker
  render={({ x, y }) => (
    <p>
      {x}, {y}
    </p>
  )}
/>;
```

The `children` prop is often used as the render function:

```tsx
<MouseTracker>
  {({ x, y }) => (
    <p>
      {x}, {y}
    </p>
  )}
</MouseTracker>
```

**Render props vs HOCs:** both share logic. Render props are more explicit (no injected props, no name collisions) but can cause **callback nesting** ("pyramid").

**Modern take:** **custom hooks** superseded most render props too — `const pos = useMouse()` is flatter and composable. Render props still shine when the shared logic must **wrap and control rendering** (e.g. virtualized list libraries, `<Formik>`, headless UI components).
