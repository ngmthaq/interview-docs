# 18. How do you manage state with Pinia in Nuxt? (Mid)

For complex shared state, Nuxt uses **Pinia** (the official Vue store) via the `@pinia/nuxt` module — SSR-friendly out of the box.

```ts
// stores/cart.ts
export const useCartStore = defineStore("cart", () => {
  const items = ref<CartItem[]>([]);

  const total = computed(() => items.value.reduce((sum, i) => sum + i.price * i.qty, 0));

  function addItem(item: CartItem) {
    items.value.push(item);
  }

  return { items, total, addItem };
});
```

Use it in components:

```vue
<script setup>
const cart = useCartStore();
cart.addItem({ id: 1, price: 9.99, qty: 2 });
</script>
```

**Notes:**

- Add `"@pinia/nuxt"` to `modules`; stores in `stores/` are auto-imported.
- Pinia handles **SSR hydration** — server state serializes to the client automatically.
- `useState` suits lightweight state; **Pinia** suits structured stores with getters/actions across many components.

**Key point:** use Pinia (`@pinia/nuxt`) for structured shared state — `defineStore` with state/getters/actions, auto-imported from `stores/`, with automatic SSR hydration; prefer it over `useState` once state grows beyond a few simple values.
