# 3. What are directives? (Fresher)

Directives are special `v-` attributes that apply **reactive behavior** to the DOM. When their expression changes, Vue updates the element.

**Core built-in directives:**

| Directive                   | Purpose                           |
| --------------------------- | --------------------------------- |
| `v-bind` (`:`)              | bind an attribute/prop            |
| `v-on` (`@`)                | attach an event listener          |
| `v-model`                   | two-way binding on form inputs    |
| `v-if`/`v-else`/`v-else-if` | conditional rendering             |
| `v-show`                    | toggle visibility (CSS `display`) |
| `v-for`                     | render a list                     |
| `v-html`                    | set raw innerHTML                 |
| `v-text`                    | set textContent                   |
| `v-once`                    | render once, then skip updates    |
| `v-pre`                     | skip compilation for this element |

```vue
<template>
  <p v-if="loggedIn">Welcome</p>
  <p v-else>Please log in</p>
  <li v-for="item in items" :key="item.id">{{ item.name }}</li>
  <input v-model="query" />
</template>
```

**Modifiers** — suffixes that change behavior (`.prevent`, `.stop`, `.once`, `.lazy`):

```vue
<form @submit.prevent="onSubmit">
<input v-model.trim.number="age" />
```

**Arguments** — after a colon: `v-bind:href`, `v-on:click`.

**Custom directives** — for low-level DOM access (e.g. `v-focus`):

```ts
app.directive("focus", { mounted: (el) => el.focus() });
```
