# 30. Async components, Suspense, and performance? (Senior)

**Async components** — load a component **lazily**, splitting it into its own bundle chunk fetched on demand:

```ts
import { defineAsyncComponent } from "vue";

const Dashboard = defineAsyncComponent(() => import("./Dashboard.vue"));
```

With loading/error states and delay:

```ts
const Comp = defineAsyncComponent({
  loader: () => import("./Heavy.vue"),
  loadingComponent: Spinner,
  errorComponent: ErrorView,
  delay: 200, // wait before showing spinner
  timeout: 5000,
});
```

**`<Suspense>`** — coordinate async dependencies (async components or a `setup` that returns a promise), showing a fallback until they resolve:

```vue
<template>
  <Suspense>
    <template #default><AsyncDashboard /></template>
    <template #fallback><Spinner /></template>
  </Suspense>
</template>
```

An `async setup()` lets a component `await` data before rendering; `<Suspense>` shows the fallback meanwhile.

**Other performance techniques:**

- **Route-level code splitting** — `component: () => import('./Page.vue')` in the router.
- **`v-once` / `v-memo`** — skip re-rendering static or unchanged subtrees.
- **`shallowRef` / `shallowReactive`** — avoid deep reactivity on large data.
- **`<keep-alive>`** — cache expensive components across toggles.
- **Virtual scrolling** — render only visible list items (e.g. `vue-virtual-scroller`).
- **Computed caching** — derive values with `computed`, not methods.

**Key idea:** ship less JS up front (async components + splitting), do less work per update (memoization, shallow reactivity), and re-render less (keep-alive, stable keys).
