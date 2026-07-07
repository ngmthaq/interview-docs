# 10. How do you manage shared state with useState? (Junior)

**`useState`** is Nuxt's built-in composable for **SSR-friendly shared state**. Unlike a plain `ref` at module scope, it's serialized on the server and hydrated on the client — and shared across components.

```ts
// composables/useAuth.ts
export function useAuthUser() {
  return useState<User | null>("auth-user", () => null);
}
```

```vue
<script setup>
const user = useAuthUser(); // same state everywhere it's called
user.value = { id: 1, name: "Ada" };
</script>
```

**Why not a module-level `ref`?**

- A module-scoped `ref` is **shared across requests** on the server → **cross-request state leakage** between users. `useState` scopes state per request.

**Key facts:**

- First arg is a **unique key**; second is an initializer.
- Values must be **serializable** (they cross the server→client boundary).
- For complex apps, use **Pinia** instead; `useState` fits lightweight shared state.

**Key point:** `useState(key, init)` provides SSR-safe, per-request shared state that hydrates correctly — use it instead of module-level refs (which leak state across requests on the server); reach for Pinia when state grows complex.
