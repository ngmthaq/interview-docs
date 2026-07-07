# 20. Composables? (Mid)

A composable is a **function that uses the Composition API to encapsulate and reuse stateful logic** — Vue's equivalent of React custom hooks. Convention: name starts with `use`.

```ts
// useMouse.ts
import { ref, onMounted, onUnmounted } from "vue";

export function useMouse() {
  const x = ref(0);
  const y = ref(0);

  function update(e: MouseEvent) {
    x.value = e.pageX;
    y.value = e.pageY;
  }

  onMounted(() => window.addEventListener("mousemove", update));
  onUnmounted(() => window.removeEventListener("mousemove", update));

  return { x, y };
}
```

**Usage** — clean, and each caller gets isolated state:

```vue
<script setup lang="ts">
import { useMouse } from "./useMouse";
const { x, y } = useMouse();
</script>
```

**A data-fetching composable:**

```ts
export function useFetch<T>(url: string) {
  const data = ref<T | null>(null);
  const error = ref<Error | null>(null);
  fetch(url)
    .then((r) => r.json())
    .then((d) => (data.value = d))
    .catch((e) => (error.value = e));
  return { data, error };
}
```

**Why composables beat mixins (Vue 2):**

- **No naming collisions** — returns are explicit.
- **Clear source** — you see where each value comes from.
- **Composable** — combine multiple `use*` functions freely.

**Guidelines:** return refs (let the caller destructure), register lifecycle hooks inside, keep each composable focused on one concern.
