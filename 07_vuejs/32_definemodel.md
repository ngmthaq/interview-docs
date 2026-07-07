# 32. What is defineModel? (Mid)

**`defineModel`** (Vue 3.4+) is a macro that dramatically simplifies building components with **`v-model`** support — replacing the old `props` + `emit('update:modelValue')` boilerplate.

**Before (verbose):**

```vue
<script setup>
const props = defineProps(["modelValue"]);
const emit = defineEmits(["update:modelValue"]);
// must read props.modelValue and emit updates manually
</script>
```

**After (`defineModel`):**

```vue
<script setup>
const model = defineModel(); // a writable ref two-way bound to v-model
</script>

<template>
  <input v-model="model" />
</template>
```

The parent uses it exactly like a native input:

```vue
<CustomInput v-model="username" />
```

**Named and multiple models:**

```ts
const firstName = defineModel("firstName");
const lastName = defineModel("lastName");
// Parent: <UserForm v-model:firstName="a" v-model:lastName="b" />
```

**Options** — type, required, default, and modifiers:

```ts
const model = defineModel<string>({ required: true });
const [count, modifiers] = defineModel<number>({ set: (v) => v }); // access .trim etc.
```

**Key point:** `defineModel()` returns a writable ref wired to the parent's `v-model`, eliminating the `modelValue` prop + `update:modelValue` emit boilerplate; it supports named models (`defineModel('name')`) for multiple `v-model` bindings and typed/required options.
