# 14. Slots? (Mid)

Slots let a parent **inject content into a child's template** — the basis of composition and reusable layout components.

**Default slot:**

```vue
<!-- Card.vue -->
<template>
  <div class="card"><slot /></div>
</template>

<!-- usage -->
<Card>
  <p>Any content goes into the slot</p>
</Card>
```

**Named slots** — multiple insertion points:

```vue
<!-- Layout.vue -->
<template>
  <header><slot name="header" /></header>
  <main><slot /></main>
  <footer><slot name="footer" /></footer>
</template>

<!-- usage -->
<Layout>
  <template #header><h1>Title</h1></template>
  <p>Main content (default slot)</p>
  <template #footer><small>© 2024</small></template>
</Layout>
```

**Scoped slots** — the child passes data **back up** to the slot content, letting the parent control rendering while the child owns the data:

```vue
<!-- List.vue -->
<template>
  <li v-for="item in items" :key="item.id">
    <slot :item="item" :index="item.id" />
  </li>
</template>

<!-- usage -->
<List :items="users">
  <template #default="{ item }">
    <strong>{{ item.name }}</strong>
  </template>
</List>
```

**Fallback content:** `<slot>Default text</slot>` renders when nothing is provided.

**Use cases:** layout wrappers, tables/lists with custom row rendering, headless/renderless components. Scoped slots are Vue's answer to React's render props.
