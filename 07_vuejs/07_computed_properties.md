# 7. Computed properties? (Fresher)

A computed property is a **derived value** that automatically recalculates when its reactive dependencies change — and is **cached** until they do.

```vue
<script setup lang="ts">
import { ref, computed } from "vue";

const firstName = ref("Ada");
const lastName = ref("Lovelace");

const fullName = computed(() => `${firstName.value} ${lastName.value}`);
</script>

<template>
  <p>{{ fullName }}</p>
</template>
```

**Caching is the key feature.** A computed re-evaluates **only when a dependency changes**. Accessing it repeatedly returns the cached result — unlike a method, which runs every call:

```vue
<p>{{ fullName }}</p>
<!-- method: runs every render -->
<p>{{ getFullName() }}</p>
```

**Writable computed** — provide `get` and `set`:

```ts
const fullName = computed({
  get: () => `${firstName.value} ${lastName.value}`,
  set: (val) => {
    [firstName.value, lastName.value] = val.split(" ");
  },
});
fullName.value = "Grace Hopper"; // triggers the setter
```

**Rules:**

- Keep computeds **pure** — no side effects, no mutating other state.
- Don't do async work in a computed (use `watch`).

**computed vs method:** computed = cached derived value; method = runs on demand. Prefer computed for values shown in the template.
