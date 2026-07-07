# 6. `v-model` and two-way binding? (Fresher)

`v-model` creates **two-way binding** between a form input and state — it's syntactic sugar over `:value` + `@input`.

```vue
<input v-model="name" />
<!-- equivalent to: -->
<input :value="name" @input="name = $event.target.value" />
```

Works with all form controls:

```vue
<input v-model="text" />
<textarea v-model="message" />
<input type="checkbox" v-model="checked" />
<select v-model="selected">...</select>
```

**Modifiers:**

- `.lazy` — sync on `change` instead of `input`.
- `.number` — cast to a number.
- `.trim` — strip whitespace.

```vue
<input v-model.number.trim="age" />
```

**`v-model` on components** — a child can be `v-model`-bound. In Vue 3 it maps to a `modelValue` prop + `update:modelValue` event:

```vue
<!-- parent -->
<CurrencyInput v-model="price" />

<!-- child -->
<script setup lang="ts">
defineProps<{ modelValue: number }>();
const emit = defineEmits<{ "update:modelValue": [value: number] }>();
</script>
<template>
  <input :value="modelValue" @input="emit('update:modelValue', +$event.target.value)" />
</template>
```

**Multiple v-models:** `v-model:title` / `v-model:content` bind several values on one component.
