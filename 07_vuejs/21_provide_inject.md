# 21. `provide` / `inject`? (Mid)

`provide`/`inject` pass data from an ancestor to any descendant **without prop drilling** — Vue's dependency injection. Analogous to React Context.

**Provide** in an ancestor:

```vue
<script setup lang="ts">
import { provide, ref } from "vue";

const theme = ref<"light" | "dark">("dark");
provide("theme", theme); // key + value
</script>
```

**Inject** in any descendant, however deep:

```vue
<script setup lang="ts">
import { inject } from "vue";
const theme = inject("theme", "light"); // key + optional default
</script>
```

**Type-safe keys** with `InjectionKey`:

```ts
import type { InjectionKey, Ref } from "vue";
export const themeKey = Symbol() as InjectionKey<Ref<string>>;

provide(themeKey, theme); // typed
const theme = inject(themeKey); // Ref<string> | undefined
```

**Reactivity:** provide a **ref/reactive** so descendants get live updates. Keep mutations in the provider and expose an updater to enforce one-way flow:

```ts
provide("theme", {
  theme: readonly(theme), // consumers can't mutate directly
  setTheme: (t) => (theme.value = t),
});
```

**When to use:**

- Theme, locale, current user, form context — cross-cutting data used by many nested components.

**vs Pinia:** `provide/inject` is scoped to a component subtree and great for library/component-internal DI. For **app-wide** shared state, prefer a **Pinia** store.
