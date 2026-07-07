# 22. Component communication patterns? (Mid)

How components share data depends on their **relationship**.

**Parent → Child: props**

```vue
<Child :user="user" />
```

**Child → Parent: emit**

```vue
<Child @update="onUpdate" />
```

**Two-way: `v-model`** (props + emit combined)

```vue
<CurrencyInput v-model="price" />
```

**Ancestor → deep descendant: `provide`/`inject`** — skip intermediate layers.

**Template ref → child instance** — call exposed methods directly:

```vue
<script setup lang="ts">
import { ref } from "vue";
const childRef = ref();
childRef.value?.reset(); // child must defineExpose({ reset })
</script>
<template><Child ref="childRef" /></template>
```

**Sibling / distant / global state: Pinia store** — the scalable answer for shared state.

**Attribute fallthrough / `$attrs`** — pass non-prop attributes and listeners through a wrapper component.

**Decision guide:**

| Relationship           | Use                           |
| ---------------------- | ----------------------------- |
| Parent ↔ direct child  | props + emit / `v-model`      |
| Ancestor → descendants | `provide` / `inject`          |
| Parent calls child API | template ref + `defineExpose` |
| Siblings / app-wide    | Pinia store                   |

**Anti-pattern:** deep **emit chains** (bubbling an event up many levels) or a homegrown event bus. Prefer lifting state up, `provide/inject`, or a store.
