# 11. Event handling and modifiers? (Fresher)

Listen to events with `v-on` (shorthand `@`). The handler can be a method or an inline expression.

```vue
<button @click="count++">Inline</button>
<button @click="handleClick">Method</button>
<button @click="handleClick($event, item)">With args</button>
```

`$event` gives access to the native event object in inline handlers.

**Event modifiers** — express common event logic declaratively instead of in the handler:

| Modifier   | Effect                                |
| ---------- | ------------------------------------- |
| `.prevent` | `event.preventDefault()`              |
| `.stop`    | `event.stopPropagation()`             |
| `.self`    | only if `event.target` is the element |
| `.once`    | fire at most once                     |
| `.capture` | use capture phase                     |
| `.passive` | `{ passive: true }` (scroll perf)     |

```vue
<form @submit.prevent="onSubmit">
<a @click.stop.prevent="doThis">
<div @click.self="onlyMe">
```

**Key modifiers** — filter keyboard events:

```vue
<input @keyup.enter="submit" />
<input @keyup.esc="cancel" />
<input @keyup.ctrl.s="save" />
```

**Mouse modifiers:** `.left`, `.right`, `.middle`.

**Why modifiers matter:** they keep handlers focused on **logic**, not DOM plumbing — no `e.preventDefault()` scattered everywhere, and chaining (`.stop.prevent`) is concise.

**Component events:** children emit custom events with `emit`; the parent listens with `@my-event` (see the emits question).
