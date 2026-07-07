# 9. Methods vs computed vs watch? (Fresher)

Three ways to handle logic — pick by intent.

|              | Purpose                   | Cached | Triggered by              |
| ------------ | ------------------------- | ------ | ------------------------- |
| **method**   | run logic on demand       | ❌     | you call it (event, etc.) |
| **computed** | derive a value from state | ✅     | dependency change         |
| **watch**    | react with a side effect  | ❌     | source change             |

```vue
<script setup lang="ts">
import { ref, computed, watch } from "vue";

const price = ref(100);
const qty = ref(2);

// computed: derived, cached value
const total = computed(() => price.value * qty.value);

// method: called explicitly
function applyDiscount() {
  price.value *= 0.9;
}

// watch: side effect on change
watch(total, (v) => console.log("total changed:", v));
</script>
```

**Decision guide:**

- Need a **value** to display that depends on state → **computed** (cached, no side effects).
- Need to **do something** in response to an event → **method**.
- Need to **react to a change** with a side effect (fetch, log, sync) → **watch**.

**Common mistake:** using a method in the template for a derived value that's recomputed every render — use a **computed** so it's cached. Conversely, don't put async/side-effect logic in a computed — use **watch**.
