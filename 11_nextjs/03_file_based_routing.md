# 3. How does file-based routing work? (Fresher)

In the **App Router**, the folder structure under `app/` **defines your routes**. Special files inside each folder have reserved meanings.

```
app/
├── page.tsx            →  /
├── about/
│   └── page.tsx        →  /about
├── blog/
│   ├── page.tsx        →  /blog
│   └── [slug]/
│       └── page.tsx    →  /blog/:slug
└── dashboard/
    ├── layout.tsx      →  wraps all /dashboard/* routes
    └── settings/
        └── page.tsx    →  /dashboard/settings
```

**Special files:**

- **`page.tsx`** — the UI for a route (makes the segment publicly routable).
- **`layout.tsx`** — shared UI wrapping child routes (persists across navigation).
- **`loading.tsx`** — Suspense fallback shown while the segment loads.
- **`error.tsx`** — error boundary for the segment.
- **`not-found.tsx`** — 404 UI.
- **`route.ts`** — an API endpoint (Route Handler) instead of a page.

**Key point:** folders under `app/` become URL segments and reserved files (`page`, `layout`, `loading`, `error`, `not-found`, `route`) define each segment's UI and behavior — routing is expressed entirely through the file system.
