# 1. What is Vue.js? (Fresher)

Vue is a **progressive JavaScript framework** for building UIs. "Progressive" means you can adopt it incrementally — drop it into one page, or build a full SPA with routing and state management.

**Core ideas:**

- **Declarative rendering** — describe the UI as a function of state; Vue keeps the DOM in sync.
- **Reactivity** — when data changes, the view updates automatically.
- **Component-based** — build UIs from reusable, self-contained components.

```vue
<script setup lang="ts">
import { ref } from "vue";
const count = ref(0);
</script>

<template>
  <button @click="count++">Count: {{ count }}</button>
</template>
```

**Single-File Components (SFC)** — a `.vue` file bundles `<template>`, `<script>`, and `<style>` for one component, keeping related concerns together.

**vs React/Angular:**

- Lighter and more approachable than Angular; less boilerplate than React.
- **Templates** (HTML-based) instead of JSX (though JSX is supported).
- Built-in reactivity, transitions, and official router/state libraries.

**Vue 2 vs Vue 3:** Vue 3 (the current default) rewrote the reactivity system with **Proxies**, added the **Composition API**, better TypeScript support, and smaller bundles.
