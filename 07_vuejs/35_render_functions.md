# 35. What are render functions and the h() function? (Senior)

Instead of a `<template>`, you can define a component's output **programmatically** with a **render function** using **`h()`** (hyperscript — creates virtual DOM nodes). Useful when template syntax is too limiting.

```ts
import { h } from "vue";

export default {
  props: ["level", "text"],
  setup(props) {
    // Dynamic tag name — awkward in templates, trivial here
    return () => h(`h${props.level}`, { class: "title" }, props.text);
  },
};
```

**`h(type, props, children)`:**

```ts
h("div", { id: "app", onClick: handler }, [h("span", "Hello"), h(MyComponent, { msg: "hi" })]);
```

**When to use render functions:**

- **Fully dynamic** structure (variable tag names, programmatically generated children).
- Highly **reusable, logic-heavy** components (e.g. a table/renderer library).
- When template directives can't express the logic cleanly.

**JSX** is an alternative syntax for the same thing (via `@vitejs/plugin-vue-jsx):

```tsx
setup(props) {
  return () => <div class="title">{props.text}</div>;
}
```

**Trade-off:** render functions/JSX give full JavaScript power but lose the template's compile-time optimizations and readability — prefer templates for most components.

**Key point:** render functions return `h(type, props, children)` VDOM instead of a template, giving full programmatic control (dynamic tags, generated children) — ideal for highly dynamic/library components; JSX is an equivalent syntax, but templates remain preferred for readability and compiler optimizations.
