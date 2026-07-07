# 12. What is route middleware in Nuxt? (Junior)

**Route middleware** runs **before navigating** to a route — ideal for auth guards, redirects, and access checks. It's defined in the **`middleware/`** directory.

```ts
// middleware/auth.ts
export default defineNuxtRouteMiddleware((to, from) => {
  const user = useAuthUser();
  if (!user.value) {
    return navigateTo("/login"); // redirect
  }
});
```

Apply it to a page:

```vue
<script setup>
definePageMeta({ middleware: "auth" });
</script>
```

**Three kinds:**

- **Named** — files in `middleware/`, referenced by name in `definePageMeta`.
- **Global** — files suffixed `.global.ts` run on **every** route change automatically.
- **Inline** — defined directly in `definePageMeta({ middleware: [...] })`.

**Notes:**

- Runs on both **server (first load)** and **client (navigation)** — keep it isomorphic.
- Return `navigateTo(...)` or `abortNavigation()` to control the flow.

**Key point:** route middleware (`defineNuxtRouteMiddleware`) runs before navigation for auth/redirect logic — named (in `middleware/`), global (`.global.ts`), or inline; it runs on both server and client, and returns `navigateTo`/`abortNavigation` to redirect or block.
