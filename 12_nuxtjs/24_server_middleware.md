# 24. Server middleware vs route middleware. (Senior)

Nuxt has **two distinct middleware systems** — a common point of confusion.

**Route middleware** (`middleware/`) — runs in the **Vue/navigation** layer, before rendering a route (client + server):

```ts
// middleware/auth.ts — controls page navigation
export default defineNuxtRouteMiddleware((to) => {
  if (!useAuthUser().value) return navigateTo("/login");
});
```

**Server middleware** (`server/middleware/`) — runs in **Nitro** on **every server request**, before route handlers:

```ts
// server/middleware/logger.ts — runs for every API/page request
export default defineEventHandler((event) => {
  console.log(`${event.method} ${event.path}`);
  // e.g. attach user to event.context after verifying a token
});
```

|          | Route middleware             | Server middleware                 |
| -------- | ---------------------------- | --------------------------------- |
| Layer    | Vue Router (navigation)      | Nitro (HTTP request)              |
| Runs on  | Server (first load) + client | Server only, every request        |
| Location | `middleware/`                | `server/middleware/`              |
| Use      | Auth redirects, page guards  | Logging, headers, request context |

**Key point:** route middleware (`middleware/`, `defineNuxtRouteMiddleware`) guards **navigation** on client+server, while server middleware (`server/middleware/`, `defineEventHandler`) runs on **every server request** in Nitro for logging/headers/context — different layers for different jobs.
