# 4. `v-if` vs `v-show`? (Fresher)

Both conditionally display an element, but they work differently.

|                       | `v-if`                    | `v-show`              |
| --------------------- | ------------------------- | --------------------- |
| Mechanism             | adds/removes from **DOM** | toggles CSS `display` |
| Initial cost          | lazy — nothing if false   | always rendered       |
| Toggle cost           | high (mount/unmount)      | low (just CSS)        |
| Supports `v-else`     | ✅                        | ❌                    |
| Works on `<template>` | ✅                        | ❌                    |

```vue
<template>
  <!-- removed from DOM entirely when false -->
  <ExpensiveChart v-if="showChart" />

  <!-- stays in DOM, just hidden -->
  <div v-show="isVisible">Toggle me often</div>
</template>
```

**How to choose:**

- **`v-show`** — for elements toggled **frequently** (tabs, dropdowns). Cheap toggles; pays the render cost once.
- **`v-if`** — for conditions that **rarely change** or when the block is **expensive** and often not needed. Avoids rendering until required.

**Gotcha — `v-if` with `v-for`:** avoid on the same element; `v-if` has higher priority and the semantics are confusing. Filter with a computed property instead, or wrap in a `<template v-if>`.

**Mental model:** `v-if` is a real conditional (build vs skip); `v-show` always builds and just hides.
