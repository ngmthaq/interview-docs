# 28. What is `StrictMode`? (Mid)

`<StrictMode>` is a **development-only** helper that surfaces potential bugs. It renders nothing and has **zero effect in production**.

```tsx
createRoot(document.getElementById("root")!).render(
  <StrictMode>
    <App />
  </StrictMode>,
);
```

**What it does (dev only):**

- **Double-invokes** render, `useState`/`useMemo`/`useReducer` initializers, and **effects** (mount → unmount → mount) to expose impure logic and missing cleanup.
- Warns about **deprecated APIs** (legacy string refs, old lifecycle methods).
- Detects **unexpected side effects** during render.

**Why effects run twice:** it simulates a component **mounting, unmounting, and remounting** to verify your effect **cleans up properly**. If a subscription/timer isn't cleaned up, the double-run reveals the leak.

```tsx
useEffect(() => {
  const id = setInterval(tick, 1000);
  return () => clearInterval(id); // ← without this, double-run leaks timers
}, []);
```

**Common misconception:** "my effect/log fires twice — bug!" No — that's Strict Mode in dev. It won't happen in production. The correct response is to make the effect **idempotent and self-cleaning**, not to remove Strict Mode.

**Takeaway:** keep it on. It's a free correctness check that future-proofs components for concurrent features.
