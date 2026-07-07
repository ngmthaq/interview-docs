# 31. useLayoutEffect vs useEffect. (Mid)

Both run side effects after render, but at **different times** relative to the browser paint.

- **`useEffect`** — runs **asynchronously after paint**. The browser shows the updated DOM, then the effect fires. Non-blocking.
- **`useLayoutEffect`** — runs **synchronously after DOM mutations but before paint**. It blocks painting until it finishes.

```tsx
function Tooltip() {
  const ref = useRef<HTMLDivElement>(null);
  const [pos, setPos] = useState(0);

  // Measure & reposition BEFORE the user sees the frame — no flicker
  useLayoutEffect(() => {
    const { height } = ref.current!.getBoundingClientRect();
    setPos(-height); // adjust before paint
  }, []);

  return <div ref={ref} style={{ transform: `translateY(${pos}px)` }} />;
}
```

**When to use `useLayoutEffect`:**

- **Measuring DOM** (size/position) and synchronously re-rendering to avoid a visible flicker.
- Synchronizing scroll position or imperative DOM adjustments before paint.

**Caution:** it **blocks paint**, so overuse hurts performance. Default to `useEffect`; reach for `useLayoutEffect` only to prevent visual flicker. (It also warns during SSR since there's no layout on the server.)

**Key point:** `useEffect` runs after paint (non-blocking, the default); `useLayoutEffect` runs before paint (blocking) — use the latter only when you must read layout and mutate synchronously to prevent a visible flicker, since it delays rendering.
