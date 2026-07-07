# 12. How do loading UI and streaming work? (Junior)

The App Router streams HTML, letting you show **instant loading states** while slower data resolves — powered by React **Suspense**.

**`loading.tsx`** — automatic Suspense boundary for a route segment:

```tsx
// app/dashboard/loading.tsx — shown instantly while page.tsx awaits data
export default function Loading() {
  return <Spinner />;
}
```

**Manual streaming with `<Suspense>`** — stream parts independently:

```tsx
import { Suspense } from "react";

export default function Page() {
  return (
    <section>
      <Header /> {/* renders immediately */}
      <Suspense fallback={<SkeletonFeed />}>
        <Feed /> {/* slow async component streams in when ready */}
      </Suspense>
    </section>
  );
}
```

**Benefits:**

- The shell (layout + fast content) appears **immediately**; slow sections fill in.
- Improves perceived performance and Core Web Vitals (faster TTFB/FCP).

**Key point:** `loading.tsx` auto-wraps a segment in Suspense for an instant fallback, and manual `<Suspense>` boundaries stream slow components independently — the server sends the fast shell first and progressively streams the rest.
