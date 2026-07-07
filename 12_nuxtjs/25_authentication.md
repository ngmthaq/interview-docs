# 25. How do you implement authentication in Nuxt? (Senior)

A typical Nuxt auth setup spans **cookies**, **route middleware**, **server routes**, and **shared state**.

**Session state** — SSR-safe user via a composable:

```ts
// composables/useAuth.ts
export const useAuthUser = () => useState<User | null>("user", () => null);
```

**Login** — a server route sets an httpOnly cookie:

```ts
// server/api/login.post.ts
export default defineEventHandler(async (event) => {
  const { email, password } = await readBody(event);
  const user = await verify(email, password);
  setCookie(event, "token", signJwt(user), { httpOnly: true, secure: true });
  return { user };
});
```

**Route guard** — protect pages:

```ts
// middleware/auth.ts
export default defineNuxtRouteMiddleware(() => {
  if (!useAuthUser().value) return navigateTo("/login");
});
```

**Reading the user on SSR** — server middleware verifies the cookie and populates `event.context`, then a plugin/`useFetch('/api/me')` hydrates `useAuthUser`.

**Notes:** use **httpOnly cookies** (not `localStorage`) to resist XSS; enforce real authorization in **server routes**, not just client middleware. Modules like `@sidebase/nuxt-auth` or `nuxt-auth-utils` streamline this.

**Key point:** combine httpOnly-cookie sessions (set in server routes), `useState`-backed user state, route middleware for page guards, and server middleware to verify the cookie — but enforce authorization server-side, since client middleware alone isn't a security boundary.
