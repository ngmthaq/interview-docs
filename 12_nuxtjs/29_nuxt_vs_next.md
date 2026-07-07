# 29. Nuxt vs Next.js. (Senior)

Both are full-stack meta-frameworks solving the same problems for different UI libraries.

| Aspect            | Nuxt                             | Next.js                                      |
| ----------------- | -------------------------------- | -------------------------------------------- |
| UI library        | **Vue 3**                        | **React**                                    |
| Routing           | File-based (`pages/`)            | File-based (`app/`)                          |
| Server engine     | **Nitro** (portable presets)     | Node/Edge (Vercel-optimized)                 |
| Data fetching     | `useFetch` / `useAsyncData`      | async Server Components / `fetch`            |
| Server code       | `server/` (h3)                   | Route Handlers / Server Actions              |
| Rendering control | `routeRules` (hybrid)            | per-route config / PPR                       |
| Auto-imports      | Yes (components, composables)    | No (explicit imports)                        |
| Component model   | Vue SFCs, all components hydrate | React Server Components (zero-JS by default) |

**Notable differences:**

- **RSC:** Next's Server Components ship **zero JS** for server-only parts; Nuxt uses SSR + hydration (with islands/lazy hydration as the equivalent optimization).
- **Deployment:** Nitro's presets make Nuxt exceptionally **portable**; Next is most seamless on **Vercel**.
- **DX:** Nuxt leans on auto-imports and convention; Next on explicit imports.

**Key point:** Nuxt (Vue) and Next.js (React) are equivalent full-stack frameworks — the core differences are the UI library, Next's zero-JS React Server Components vs Nuxt's SSR+islands model, and Nitro's portable deployment vs Next's Vercel-optimized story.
