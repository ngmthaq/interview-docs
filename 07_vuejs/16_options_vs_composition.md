# 16. Options API vs Composition API? (Mid)

Two ways to author components in Vue 3.

**Options API** — organize by **option type** (`data`, `methods`, `computed`, `watch`):

```vue
<script lang="ts">
export default {
  data() {
    return { count: 0 };
  },
  computed: {
    double(): number {
      return this.count * 2;
    },
  },
  methods: {
    inc() {
      this.count++;
    },
  },
};
</script>
```

**Composition API** — organize by **logical concern**, using functions:

```vue
<script setup lang="ts">
import { ref, computed } from "vue";
const count = ref(0);
const double = computed(() => count.value * 2);
function inc() {
  count.value++;
}
</script>
```

|                | Options API              | Composition API     |
| -------------- | ------------------------ | ------------------- |
| Organization   | by option kind           | by feature/concern  |
| Logic reuse    | mixins (collision-prone) | composables (clean) |
| `this`         | relies on `this`         | no `this`           |
| TypeScript     | weaker inference         | excellent           |
| Learning curve | gentler                  | steeper             |

**Why Composition API:**

- **Better logic reuse** — extract related logic into **composables** without mixin name clashes.
- **Colocation** — a feature's state, computed, and watchers live together, not scattered across options.
- **Stronger TS support**.

**When Options API is fine:** small components, teams familiar with Vue 2. Both are fully supported; `<script setup>` is the recommended default for new apps.
