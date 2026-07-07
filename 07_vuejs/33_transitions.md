# 33. How do transitions and animations work in Vue? (Mid)

Vue's built-in **`<Transition>`** and **`<TransitionGroup>`** components apply enter/leave animations by toggling CSS classes automatically.

**`<Transition>`** — animate a single element entering/leaving:

```vue
<template>
  <Transition name="fade">
    <p v-if="show">Hello</p>
  </Transition>
</template>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
```

**The six transition classes:** `-enter-from`, `-enter-active`, `-enter-to`, and the matching `-leave-*` — Vue adds/removes them around the DOM change.

**`<TransitionGroup>`** — animate lists (add/remove/reorder), with `v-for`:

```vue
<TransitionGroup name="list" tag="ul">
  <li v-for="item in items" :key="item.id">{{ item.text }}</li>
</TransitionGroup>
```

- Requires a **`key`** on each child.
- The special **`-move`** class animates repositioning when items reorder (FLIP).

**Other features:** JavaScript hooks (`@enter`, `@leave`) for JS-driven animation, `mode="out-in"` for sequential transitions, and `appear` for initial-render animation.

**Key point:** `<Transition>` animates single-element enter/leave via six auto-applied CSS classes; `<TransitionGroup>` animates keyed lists including reordering (`-move`/FLIP) — use `name` for CSS transitions or JS hooks for imperative animation, and `mode="out-in"` to sequence swaps.
