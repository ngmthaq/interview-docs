# 29. Pinia — state management? (Mid)

Pinia is the **official** state-management library for Vue 3, replacing Vuex. It's simpler, fully typed, and Composition-API friendly.

**Defining a store** (setup syntax — mirrors `<script setup>`):

```ts
import { defineStore } from "pinia";
import { ref, computed } from "vue";

export const useCounterStore = defineStore("counter", () => {
  const count = ref(0); // state
  const double = computed(() => count.value * 2); // getter
  function increment() {
    count.value++;
  } // action
  return { count, double, increment };
});
```

**Using it in a component:**

```vue
<script setup lang="ts">
import { useCounterStore } from "@/stores/counter";
import { storeToRefs } from "pinia";

const store = useCounterStore();
const { count, double } = storeToRefs(store); // keep reactivity when destructuring
store.increment();
</script>
```

**Three concepts:**

| Concept | Vuex term           | Pinia                           |
| ------- | ------------------- | ------------------------------- |
| state   | state               | `ref`s                          |
| getters | getters             | `computed`s                     |
| actions | mutations + actions | plain functions (sync or async) |

**Pinia vs Vuex:**

- **No mutations** — actions mutate state directly (less boilerplate).
- **First-class TypeScript** inference.
- **Modular by design** — each store is independent, no nested modules.
- Smaller, with better devtools and code-splitting.

**Gotcha:** destructuring a store **loses reactivity** — wrap state/getters in `storeToRefs`. Actions can be destructured directly (they're plain functions).
