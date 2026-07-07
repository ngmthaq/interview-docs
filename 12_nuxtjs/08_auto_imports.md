# 8. How do auto-imports work in Nuxt? (Junior)

Nuxt **auto-imports** components, composables, and Vue/Nuxt APIs — you use them without writing `import` statements.

```vue
<script setup>
// No imports needed for any of these:
const count = ref(0); // Vue API
const route = useRoute(); // Nuxt composable
const { data } = await useFetch("/api/x"); // Nuxt composable

onMounted(() => console.log("mounted")); // Vue lifecycle
</script>

<template>
  <MyComponent />
  <!-- components/MyComponent.vue auto-imported -->
</template>
```

**What's auto-imported:**

- **Vue APIs** — `ref`, `computed`, `reactive`, `watch`, lifecycle hooks.
- **Nuxt composables** — `useFetch`, `useAsyncData`, `useState`, `useRoute`, `navigateTo`, etc.
- **Your `components/`** — by file name (nested folders prefix the name).
- **Your `composables/`** and **`utils/`** — auto-imported by their exported names.

**Benefits & notes:**

- Less boilerplate; **tree-shaking** still removes unused code.
- Explicit imports from `#imports` are available if you prefer them or for clarity.

**Key point:** Nuxt auto-imports Vue APIs, its own composables, and your `components/`/`composables/`/`utils/` by convention — reducing boilerplate while keeping tree-shaking; you can still import explicitly from `#imports` when desired.
