# 15. Lifecycle hooks? (Mid)

Lifecycle hooks run code at specific stages of a component's life. In the Composition API they are functions imported and called inside `setup`.

```vue
<script setup lang="ts">
import { onMounted, onUnmounted, onUpdated } from "vue";

onMounted(() => {
  // DOM is ready — fetch data, init libraries, add listeners
});
onUnmounted(() => {
  // cleanup — remove listeners, clear timers
});
</script>
```

**Main hooks (Composition API ↔ Options API):**

| Composition       | Options API              | When                            |
| ----------------- | ------------------------ | ------------------------------- |
| `setup`           | `beforeCreate`/`created` | before mount, state set up      |
| `onBeforeMount`   | `beforeMount`            | before first render to DOM      |
| `onMounted`       | `mounted`                | after mounted to DOM            |
| `onBeforeUpdate`  | `beforeUpdate`           | before re-render on data change |
| `onUpdated`       | `updated`                | after DOM re-rendered           |
| `onBeforeUnmount` | `beforeUnmount`          | before teardown                 |
| `onUnmounted`     | `unmounted`              | after teardown — do cleanup     |

```ts
onMounted(() => {
  const id = setInterval(tick, 1000);
  onUnmounted(() => clearInterval(id)); // colocate setup + cleanup
});
```

**Common uses:**

- `onMounted` — API calls, accessing DOM/refs, third-party libs.
- `onUnmounted` — remove event listeners, clear intervals, close sockets.

**keep-alive hooks:** `onActivated` / `onDeactivated` fire when a cached component is shown/hidden.

**Note:** `<script setup>` code itself runs at the `created` stage — no separate `created` hook needed.
