# 13. Custom events (`emits`)? (Fresher)

A child sends data **up** to its parent by **emitting events**. This completes the loop: props down, events up.

**Declaring and emitting** with `<script setup>`:

```vue
<script setup lang="ts">
const emit = defineEmits<{
  submit: [payload: { id: number }]; // typed events
  close: [];
}>();

function onSave() {
  emit("submit", { id: 1 });
}
</script>

<template>
  <button @click="onSave">Save</button>
  <button @click="emit('close')">Close</button>
</template>
```

**Parent listens** with `@`:

```vue
<EditForm @submit="handleSubmit" @close="handleClose" />
```

**Why declare emits?** Declared events:

- Document the component's API.
- Are **not** applied to the root DOM element as fallthrough attributes.
- Get TypeScript type-checking on payloads.

**`v-model` is built on this** — `emit('update:modelValue', value)` + a `modelValue` prop.

**Event validation** (runtime form):

```ts
const emit = defineEmits({
  submit: (payload: unknown) => payload != null, // return false to warn
});
```

**Naming:** emit in `camelCase` or `kebab-case`; listen in `kebab-case` in templates (`@my-event`). Vue auto-converts.

**Pattern:** for sibling/distant communication, don't chain emits everywhere — lift state up or use a store (Pinia).
