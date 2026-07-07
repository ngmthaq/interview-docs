# 18. `<script setup>`? (Mid)

`<script setup>` is compile-time syntactic sugar for the Composition API — the recommended way to write SFCs. Everything at the top level is **automatically exposed** to the template.

```vue
<script setup lang="ts">
import { ref } from "vue";
import ChildComp from "./ChildComp.vue";

const count = ref(0); // available in template
function inc() {
  count.value++;
} // available in template
</script>

<template>
  <ChildComp />
  <!-- imported components: no registration needed -->
  <button @click="inc">{{ count }}</button>
</template>
```

**Advantages over plain `setup()`:**

- **Less boilerplate** — no `return {}`, no `components: {}` registration.
- **Better performance** — more compile-time optimization.
- **Better TypeScript** and IDE support.

**Compiler macros** (no import needed, compiled away):

| Macro          | Purpose                          |
| -------------- | -------------------------------- |
| `defineProps`  | declare props                    |
| `defineEmits`  | declare emitted events           |
| `defineExpose` | expose members to parent refs    |
| `withDefaults` | default values for typed props   |
| `defineModel`  | two-way `v-model` binding (3.4+) |

```ts
const props = defineProps<{ id: number }>();
const emit = defineEmits<{ update: [value: string] }>();
defineExpose({ reset }); // parent can call via template ref
```

**Note:** components using `<script setup>` are **closed by default** — internals aren't accessible via a template ref unless you `defineExpose` them.
