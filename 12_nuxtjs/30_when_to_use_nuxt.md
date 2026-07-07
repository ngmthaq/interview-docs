# 30. When should you (not) use Nuxt? (Senior)

Choosing Nuxt is about fit — knowing the trade-offs signals maturity.

**Use Nuxt when:**

- You're building with **Vue** and need **SEO / fast first paint** — SSR delivers full HTML (marketing, e-commerce, blogs, content sites).
- You want a **full-stack** app — UI plus a backend (`server/`) in one project.
- You need **flexible per-route rendering** (SSG/SSR/SPA/ISR via `routeRules`) and **portable deployment** (Nitro presets).
- You value **convention + auto-imports** to move fast with a consistent structure.

**Reconsider when:**

- Building a **purely client-side, auth-gated SPA** with no SEO need — plain **Vue + Vite** is lighter and simpler.
- The team prefers **explicit, minimal magic** — Nuxt's auto-imports and conventions add abstraction to learn.
- You need a **specific backend architecture** better served by a dedicated API (NestJS/Go) with a separate Vue frontend.
- **Static-only** content with no app logic — a simpler SSG (VitePress/Astro) may suffice.

**Key point:** choose Nuxt for SEO-sensitive, content-rich, or full-stack **Vue** apps needing flexible rendering and portable deployment; skip it for SEO-free internal SPAs, static-only sites, or when a dedicated separate backend fits better — weigh its convention/auto-import learning curve.
