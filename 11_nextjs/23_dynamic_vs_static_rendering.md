# 23. Static vs dynamic rendering — how does Next.js decide? (Senior)

Next.js **automatically** chooses between static (rendered at build) and dynamic (rendered per request) based on what a route uses. Knowing the triggers is key.

**A route becomes dynamic if it:**

- Uses **dynamic functions** — `cookies()`, `headers()`, `draftMode()`.
- Reads **`searchParams`** in a page.
- Uses a `fetch` with **`{ cache: "no-store" }`** or `revalidate: 0`.
- Explicitly opts in via **`export const dynamic = "force-dynamic"`**.

**Otherwise it's static** (cached HTML/RSC), optionally with **ISR** if you set `revalidate`.

```tsx
// Force behavior explicitly with route segment config:
export const dynamic = "force-dynamic"; // always SSR
export const dynamic = "force-static"; // always static
export const revalidate = 3600; // ISR — revalidate hourly
export const dynamic = "error"; // fail build if anything forces dynamic
```

**Partial Prerendering (PPR)** — a newer model: serve a static shell instantly and stream dynamic holes (wrapped in Suspense) within the same route.

**Key point:** Next.js infers static vs dynamic from usage — `cookies()`/`headers()`/`searchParams`/`no-store` force dynamic, otherwise the route is static (with optional ISR); override with the `dynamic`/`revalidate` segment config, and PPR blends both in one route.
