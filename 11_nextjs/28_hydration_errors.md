# 28. What causes hydration errors and how do you fix them? (Senior)

**Hydration** is React attaching interactivity to server-rendered HTML on the client. A **hydration error** occurs when the client's first render **doesn't match** the server HTML.

**Common causes:**

- Rendering **non-deterministic values** — `Date.now()`, `Math.random()`, `new Date().toLocaleString()` — differ between server and client.
- Reading **browser-only APIs** (`window`, `localStorage`) during render.
- Invalid HTML nesting (e.g. `<div>` inside `<p>`).
- Browser extensions mutating the DOM before hydration.

**Fixes:**

```tsx
"use client";
import { useState, useEffect } from "react";

function Clock() {
  const [time, setTime] = useState<string | null>(null);
  useEffect(() => setTime(new Date().toLocaleTimeString()), []); // client-only
  if (!time) return null; // render nothing until mounted → matches server
  return <span>{time}</span>;
}
```

Other options: `suppressHydrationWarning` for unavoidable diffs (e.g. timestamps), or `next/dynamic` with `{ ssr: false }` to render a component only on the client.

**Key point:** hydration errors come from server/client render mismatches — non-deterministic values or browser-only APIs during render; fix by deferring such logic to `useEffect`, guarding on a mounted flag, using `dynamic({ ssr: false })`, or `suppressHydrationWarning` for inherently variable output.
