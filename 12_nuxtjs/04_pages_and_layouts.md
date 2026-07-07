# 4. What are pages, layouts, and app.vue? (Fresher)

Nuxt has a small hierarchy of root-level components.

**`app.vue`** — the root component, entry point of the app:

```vue
<!-- app.vue -->
<template>
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>
```

- **`<NuxtPage />`** — renders the current route's page (from `pages/`).
- **`<NuxtLayout />`** — wraps pages in a layout.

**Layouts** (`layouts/`) — shared UI wrapping pages (header, sidebar, footer):

```vue
<!-- layouts/default.vue -->
<template>
  <div>
    <AppHeader />
    <slot />
    <!-- the page renders here -->
    <AppFooter />
  </div>
</template>
```

Select a layout per page:

```vue
<script setup>
definePageMeta({ layout: "admin" }); // use layouts/admin.vue
</script>
```

`layouts/default.vue` is applied automatically when no layout is specified.

**Key point:** `app.vue` is the root (rendering `<NuxtLayout>` + `<NuxtPage>`); layouts in `layouts/` wrap pages via a `<slot />` (with `default.vue` used automatically), and pages pick a layout with `definePageMeta({ layout })`.
