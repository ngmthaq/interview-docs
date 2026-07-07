# 8. Watchers (`watch`)? (Mid)

`watch` runs a **callback with side effects** when a reactive source changes. Use it for things computed properties can't do: async calls, DOM manipulation, logging.

```vue
<script setup lang="ts">
import { ref, watch } from "vue";

const query = ref("");

watch(query, async (newVal, oldVal) => {
  const results = await search(newVal); // side effect
});
</script>
```

**Watch sources** can be a ref, a getter, or an array:

```ts
watch(() => user.id, fetchUser); // getter for reactive object prop
watch([a, b], ([newA, newB]) => {}); // multiple sources
```

**Options:**

- **`immediate: true`** — run once right away, not just on change.
- **`deep: true`** — watch nested changes in objects/arrays.
- **`flush: 'post'`** — run after the DOM updates.

```ts
watch(
  () => state.filters,
  () => refetch(),
  { deep: true, immediate: true },
);
```

**Deep watch caveat:** watching a `reactive` object is deep by default and can be expensive; prefer watching a **specific getter** when possible.

**watch vs computed:**

- **computed** — derive a new **value** (pure, cached).
- **watch** — perform a **side effect** in reaction to change.

**Stop a watcher:** `watch` returns a stop function; call it to unwatch (auto-stopped when the component unmounts).
