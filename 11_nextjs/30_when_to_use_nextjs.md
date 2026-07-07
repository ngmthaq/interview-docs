# 30. When should you (not) use Next.js? (Senior)

Choosing Next.js — like any framework — is about fit.

**Use Next.js when:**

- You need **SEO / fast first paint** — server rendering delivers full HTML (marketing sites, e-commerce, blogs, content platforms).
- You want a **full-stack React** app — UI, API (Route Handlers), and mutations (Server Actions) in one codebase.
- You want **flexible per-route rendering** (SSG/ISR/SSR) and built-in image/font/script optimization.
- You'll deploy somewhere that supports its server features (Vercel or a Node host).

**Reconsider when:**

- Building a **purely client-side, auth-gated app** (internal dashboard) with no SEO need — a plain **Vite + React SPA** is simpler and lighter.
- You need a **specific backend architecture** better served by a dedicated API (NestJS/Go) with a separate frontend.
- The team wants **minimal magic/abstraction** — Next's caching and rendering model has a real learning curve.
- **Static-only** content with no server logic — a simpler SSG (Astro) may fit better.

**Key point:** choose Next.js for SEO-sensitive, content-rich, or full-stack React apps needing flexible rendering and optimization; skip it for SEO-free internal SPAs, static-only sites, or when a dedicated separate backend suits the architecture better — weigh its rendering/caching learning curve.
