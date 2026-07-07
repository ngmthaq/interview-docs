# 21. How do environment variables work in Next.js? (Mid)

Next.js loads `.env` files automatically and distinguishes **server-only** from **browser-exposed** variables.

```bash
# .env.local
DATABASE_URL=postgres://...        # server-only (secret)
NEXT_PUBLIC_API_URL=https://api... # exposed to the browser
```

```tsx
// Server Component / Route Handler / Server Action — full access
const db = process.env.DATABASE_URL;

// Client Component — ONLY NEXT_PUBLIC_* are available
("use client");
const api = process.env.NEXT_PUBLIC_API_URL;
```

**Key rules:**

- Variables **without** `NEXT_PUBLIC_` are only available **server-side** — never shipped to the client.
- Variables prefixed **`NEXT_PUBLIC_`** are **inlined at build time** into the client bundle (so don't put secrets there, and rebuild to change them).
- Load order: `.env.local` > `.env.[environment]` > `.env`.
- `.env.local` should be git-ignored; commit a `.env.example`.

**Key point:** only `NEXT_PUBLIC_`-prefixed vars reach the browser (inlined at build time) — everything else stays server-only; never prefix secrets with `NEXT_PUBLIC_`, and remember public vars require a rebuild to change.
