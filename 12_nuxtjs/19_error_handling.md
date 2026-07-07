# 19. How do you handle errors in Nuxt? (Mid)

Nuxt handles errors at multiple levels — a global error page, thrown errors, and local error state.

**Global error page** — `error.vue` at the project root:

```vue
<!-- error.vue -->
<script setup>
const props = defineProps<{ error: { statusCode: number; message: string } }>();
const handleError = () => clearError({ redirect: "/" });
</script>

<template>
  <div>
    <h1>{{ error.statusCode }}</h1>
    <p>{{ error.message }}</p>
    <button @click="handleError">Go home</button>
  </div>
</template>
```

**Throwing errors:**

```ts
// Fatal — renders error.vue
throw createError({ statusCode: 404, statusMessage: "Not Found", fatal: true });

// In a server route
throw createError({ statusCode: 401, statusMessage: "Unauthorized" });
```

**Local handling:**

- `useFetch`/`useAsyncData` return an **`error`** ref for inline handling.
- **`<NuxtErrorBoundary>`** catches errors in a section of the UI without a full error page.
- `clearError()` resets the error state (optionally redirecting).

**Key point:** Nuxt uses a root `error.vue` for fatal errors, `createError({ statusCode, fatal })` to trigger it (also in server routes), the `error` ref from data composables for inline handling, and `<NuxtErrorBoundary>` for scoped recovery — with `clearError()` to reset.
