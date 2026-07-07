# 5. How do you navigate between pages? (Fresher)

Nuxt provides **client-side navigation** that swaps pages without a full reload.

**Declarative — `<NuxtLink>`:**

```vue
<template>
  <nav>
    <NuxtLink to="/">Home</NuxtLink>
    <NuxtLink to="/blog/hello">Blog Post</NuxtLink>
    <NuxtLink :to="{ path: '/shop', query: { sort: 'price' } }">Shop</NuxtLink>
  </nav>
</template>
```

**Programmatic — `navigateTo` / `useRouter`:**

```vue
<script setup>
async function login() {
  // navigateTo is the recommended helper (works in middleware too)
  await navigateTo("/dashboard");
}

// or the router instance
const router = useRouter();
router.push("/profile");
</script>
```

**Notes:**

- `<NuxtLink>` **prefetches** linked pages when they enter the viewport for instant navigation.
- `navigateTo()` is preferred in **route middleware** and setup, and can return redirects.
- Access the current route with **`useRoute()`** (params, query, path).

**Key point:** use `<NuxtLink to>` for declarative navigation (with automatic prefetching) and `navigateTo()` / `useRouter().push()` for programmatic navigation; read the active route with `useRoute()` — all client-side transitions preserving layouts.
