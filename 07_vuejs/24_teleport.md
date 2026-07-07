# 24. `<Teleport>`? (Mid)

`<Teleport>` renders its content at a **different place in the DOM**, outside the component's location, while keeping it logically part of the component (state, props, events stay connected). Vue's equivalent of React portals.

```vue
<template>
  <div class="component">
    <Teleport to="body">
      <div class="modal">
        <slot />
      </div>
    </Teleport>
  </div>
</template>
```

The modal markup lives in the component, but the DOM node is appended to `<body>`.

**`to`** accepts a CSS selector or an element: `to="body"`, `to="#modals"`.

**Why it exists — the CSS containment problem:** modals, tooltips, dropdowns, and toasts need to escape parents with `overflow: hidden`, `transform`, or a low `z-index` stacking context. Rendering inside a deeply nested component makes correct positioning/layering hard. Teleporting to `body` sidesteps it.

**Key behaviors:**

- **Logic stays local** — the teleported content still belongs to the component: reactive state, props, and emitted events work normally.
- **`disabled` prop** — conditionally teleport (e.g. inline on mobile, teleported on desktop):

```vue
<Teleport to="body" :disabled="isMobile">
```

- **Multiple teleports** to the same target append in order.

**Common use:** a reusable `<Modal>` component you can drop anywhere in the tree, while its overlay always renders at the document root.
