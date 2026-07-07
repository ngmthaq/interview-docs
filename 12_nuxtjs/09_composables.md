# 9. What are composables in Nuxt? (Junior)

**Composables** are reusable functions (using Vue's Composition API) that encapsulate stateful logic. Files in the **`composables/`** directory are **auto-imported**.

```ts
// composables/useCounter.ts
export function useCounter(initial = 0) {
  const count = ref(initial);
  const increment = () => count.value++;
  const decrement = () => count.value--;
  return { count, increment, decrement };
}
```

Use it anywhere without importing:

```vue
<script setup>
const { count, increment } = useCounter(10);
</script>
```

**Conventions & notes:**

- Name them **`useXxx`** by convention.
- Auto-imported from `composables/` (top-level files, and the index of subfolders).
- Great for sharing logic: data fetching, form state, auth, feature flags.
- For **shared cross-component state**, use `useState` inside a composable (SSR-friendly) rather than a module-level `ref`.

**Key point:** composables are auto-imported `useXxx` functions in `composables/` that encapsulate reusable Composition-API logic; combine with `useState` for SSR-safe shared state — Nuxt's idiomatic way to share stateful logic across components.
