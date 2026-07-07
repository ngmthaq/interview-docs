# 23. Dynamic components and `<keep-alive>`? (Mid)

**Dynamic components** — render a component chosen at runtime via `<component :is>`:

```vue
<script setup lang="ts">
import Home from "./Home.vue";
import Profile from "./Profile.vue";
import { ref, shallowRef } from "vue";

const tabs = { Home, Profile };
const current = shallowRef(Home); // or a string name
</script>

<template>
  <component :is="current" />
  <button @click="current = Profile">Profile</button>
</template>
```

`:is` accepts a component definition, an imported component, or a registered name string. Common for **tab systems** and **wizards**.

**`<keep-alive>`** — caches component instances instead of destroying them when toggled, **preserving their state** (form input, scroll position):

```vue
<template>
  <keep-alive>
    <component :is="current" />
  </keep-alive>
</template>
```

Without `keep-alive`, switching away **unmounts** the component and loses its state; switching back re-creates it fresh.

**`keep-alive` options:**

- `include` / `exclude` — cache only certain components (by name).
- `max` — limit the number of cached instances (LRU eviction).

```vue
<keep-alive :include="['Home']" :max="5">
```

**Special lifecycle hooks** for cached components:

```ts
onActivated(() => {}); // shown from cache
onDeactivated(() => {}); // hidden into cache (not unmounted)
```

**Use cases:** tabbed interfaces where re-fetching/re-rendering on every switch is wasteful, multi-step forms, and routes you want to keep alive.
