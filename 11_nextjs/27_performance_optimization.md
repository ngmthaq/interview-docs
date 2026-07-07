# 27. How do you optimize Next.js performance? (Senior)

Next.js is fast by default, but large apps need deliberate tuning.

**Rendering & JS:**

- **Minimize `"use client"`** — keep components server-side; push interactivity to leaves to shrink the bundle.
- **Dynamic imports** — lazy-load heavy client components: `next/dynamic` with `ssr: false` where appropriate.
- **Stream** slow sections with `<Suspense>`; use `loading.tsx` for instant shells.

**Assets:**

- **`next/image`** for images; **`next/font`** to self-host fonts (no layout shift, no external requests).
- **`next/script`** with the right `strategy` for third-party scripts.

**Data & caching:**

- Prefer **static/ISR** over SSR where possible; cache `fetch` results.
- Fetch in **parallel** (`Promise.all`) to avoid request waterfalls.
- Use **`@next/bundle-analyzer`** to find bloat.

**Delivery:**

- Deploy behind a **CDN/edge**; enable PPR for static-shell + dynamic streaming.

**Key point:** shrink client JS (fewer `"use client"`, dynamic imports), optimize assets (`next/image`, `next/font`, `next/script`), prefer static/ISR with cached parallel data fetching, and stream with Suspense — measure with the bundle analyzer to target real bottlenecks.
