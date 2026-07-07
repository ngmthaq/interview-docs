# 34. toRef, toRefs, and reactivity utilities. (Mid)

When you **destructure** a reactive object, the pieces **lose reactivity** — they become plain values. **`toRefs`**/**`toRef`** preserve the reactive connection.

```ts
const state = reactive({ count: 0, name: "Ada" });

// ❌ destructuring breaks reactivity
const { count } = state; // count is a plain number, not reactive

// ✅ toRefs — each property becomes a connected ref
const { count, name } = toRefs(state);
count.value++; // still updates state.count
```

**`toRef`** — a single reactive property (also works for optional/props):

```ts
const countRef = toRef(state, "count");
```

**Common use — returning reactive state from a composable:**

```ts
function useCounter() {
  const state = reactive({ count: 0 });
  const increment = () => state.count++;
  return { ...toRefs(state), increment }; // consumer can destructure safely
}
```

**Related utilities:**

- **`storeToRefs`** — Pinia's version, for destructuring store state reactively (skips actions).
- **`unref(x)`** — returns `x.value` if it's a ref, else `x`.
- **`isRef` / `isReactive`** — type checks.

**Key point:** destructuring a `reactive` object breaks reactivity; `toRefs` converts every property to a connected ref (and `toRef` a single one) so consumers can destructure safely — the standard pattern for returning reactive state from composables, with `storeToRefs` as Pinia's equivalent.
