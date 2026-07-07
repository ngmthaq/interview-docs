# 6. What rendering strategies does Next.js support? (Junior)

Next.js can render each route differently — a key selling point. The four strategies:

- **CSR (Client-Side Rendering)** — rendered in the browser (classic React SPA behavior). Good for private, highly interactive dashboards.
- **SSR (Server-Side Rendering)** — HTML generated **per request** on the server. Fresh data, good SEO; higher server cost.
- **SSG (Static Site Generation)** — HTML generated **at build time**, served from CDN. Fastest; best for content that rarely changes.
- **ISR (Incremental Static Regeneration)** — static pages **regenerated** in the background after a time interval, combining SSG speed with fresher data.

```tsx
// App Router controls this via fetch caching:
await fetch(url); // cached → static (SSG-like)
await fetch(url, { cache: "no-store" }); // per-request → SSR
await fetch(url, { next: { revalidate: 60 } }); // ISR — revalidate every 60s
```

**Choosing:**

- Marketing/blog → **SSG/ISR**.
- Personalized/frequently-changing → **SSR**.
- Private interactive app → **CSR** (client components).

**Key point:** Next.js supports CSR, SSR (per-request), SSG (build-time), and ISR (periodic regeneration) — in the App Router you select them per-`fetch` via caching/`revalidate` options, choosing based on data freshness vs performance.
