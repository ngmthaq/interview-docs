# 31. How do you create custom directives? (Mid)

**Custom directives** encapsulate **low-level DOM access** reusable across elements — when you need direct DOM manipulation that components can't cleanly express (focus, click-outside, scroll, tooltips).

```ts
// A v-focus directive
const vFocus = {
  mounted: (el: HTMLElement) => el.focus(),
};

// In <script setup>, any variable named vXxx is a directive:
// <input v-focus />
```

**Directive hooks** mirror lifecycle:

```ts
const vClickOutside = {
  mounted(el, binding) {
    el._handler = (e: Event) => {
      if (!el.contains(e.target as Node)) binding.value(e); // call the handler
    };
    document.addEventListener("click", el._handler);
  },
  unmounted(el) {
    document.removeEventListener("click", el._handler);
  },
};
// <div v-click-outside="closeMenu">
```

**Available hooks:** `created`, `beforeMount`, `mounted`, `beforeUpdate`, `updated`, `beforeUnmount`, `unmounted`.

**The `binding` object:** `value` (passed value), `arg` (`v-dir:arg`), `modifiers` (`v-dir.mod`), `oldValue`.

**Register globally** for app-wide use: `app.directive("focus", vFocus)`.

**Key point:** custom directives (`vXxx` locally or `app.directive` globally) encapsulate reusable low-level DOM behavior via lifecycle hooks (`mounted`/`unmounted`/…) and a `binding` object — use them for DOM concerns like focus, click-outside, and scroll, not for component-level logic (prefer composables there).
