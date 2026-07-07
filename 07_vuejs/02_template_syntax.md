# 2. Template syntax and interpolation? (Fresher)

Vue templates are **valid HTML** enhanced with Vue-specific syntax. Under the hood they compile to render functions.

**Text interpolation** — the "mustache" syntax:

```vue
<template>
  <p>Hello, {{ name }}</p>
  <p>{{ count * 2 }}</p>
  <!-- JS expressions allowed -->
  <p>{{ ok ? "Yes" : "No" }}</p>
</template>
```

Only **single expressions** are allowed — not statements (`if`, `for`) or declarations.

**Attribute binding** with `v-bind` (shorthand `:`):

```vue
<img :src="imageUrl" :alt="description" />
<div :class="{ active: isActive }"></div>
<button :disabled="isLoading">Save</button>
```

**Raw HTML** with `v-html` (⚠️ XSS risk — never with user input):

```vue
<div v-html="trustedHtml"></div>
```

**Event binding** with `v-on` (shorthand `@`):

```vue
<button @click="handleClick">Click</button>
```

**Key distinction:**

- `{{ }}` — text content.
- `:attr` — dynamic attributes/props.
- `@event` — event listeners.

**Note:** interpolation escapes HTML by default (safe against XSS). Use `v-html` only for content you trust.
