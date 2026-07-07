# 5. `v-for` and the `key` attribute? (Fresher)

`v-for` renders a list from an array, object, or range.

```vue
<template>
  <li v-for="(item, index) in items" :key="item.id">{{ index }}: {{ item.name }}</li>

  <!-- objects -->
  <li v-for="(value, key) in obj" :key="key">{{ key }}: {{ value }}</li>

  <!-- range -->
  <span v-for="n in 5" :key="n">{{ n }}</span>
</template>
```

**Always bind a `:key`** — a stable, unique identifier. Vue uses it to track identity across re-renders so it can **reuse and reorder** DOM nodes instead of rebuilding them.

**Why not the index as key?** On reorder/insert/delete, index keys make Vue reuse the wrong node — breaking component state, inputs, and transitions:

```vue
<template>
  <li v-for="(t, i) in todos" :key="i"><!-- ❌ breaks on reorder --></li>
  <li v-for="t in todos" :key="t.id"><!-- ✅ stable identity --></li>
</template>
```

**Array reactivity:** Vue 3 (Proxy-based) detects index assignment and `.length` changes directly. Mutating methods (`push`, `splice`, `sort`) are reactive, as is replacing the array.

**`v-for` with `v-if`:** don't combine on one element — `v-if` runs per-iteration with confusing precedence. Pre-filter with a computed:

```ts
const activeItems = computed(() => items.value.filter((i) => i.active));
```
