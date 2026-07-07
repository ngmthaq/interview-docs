# 26. Template refs? (Mid)

Template refs give you **direct access to a DOM element or child component instance**. Declare a ref and bind it with `ref="..."`.

**DOM element:**

```vue
<script setup lang="ts">
import { ref, onMounted } from "vue";
const inputEl = ref<HTMLInputElement | null>(null);

onMounted(() => inputEl.value?.focus());
</script>

<template>
  <input ref="inputEl" />
</template>
```

The ref variable must **match the `ref` attribute name**. It's `null` until the component is mounted.

**Child component instance:**

```vue
<script setup lang="ts">
const formRef = ref();
function submit() {
  formRef.value?.validate(); // call child's exposed method
}
</script>
<template>
  <MyForm ref="formRef" />
</template>
```

Because `<script setup>` components are closed, the child must **`defineExpose`** what the parent may access:

```ts
// inside MyForm
defineExpose({ validate });
```

**Refs inside `v-for`** — the ref becomes an **array** of elements/instances:

```vue
<li v-for="item in items" :key="item.id" ref="itemRefs">
```

**Function refs** — pass a function to run custom logic when the element mounts/unmounts:

```vue
<input :ref="(el) => (myInput = el)" />
```

**When to use:** focus management, measuring/scrolling DOM, integrating non-Vue libraries, calling a child's imperative API. Prefer declarative state; use refs as an escape hatch.
