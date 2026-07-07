# 17. `ref` vs `reactive`? (Mid)

Both create reactive state in the Composition API; they differ in what they wrap and how you access them.

**`ref`** — wraps **any value** (primitive or object) in a `{ value }` container:

```ts
import { ref } from "vue";
const count = ref(0);
count.value++; // .value in JS
```

**`reactive`** — makes an **object/array** deeply reactive via a Proxy; access properties directly:

```ts
import { reactive } from "vue";
const state = reactive({ count: 0, user: { name: "A" } });
state.count++; // no .value
```

|              | `ref`                | `reactive`          |
| ------------ | -------------------- | ------------------- |
| Works with   | any type             | objects/arrays only |
| Access       | `.value` (JS)        | direct property     |
| Reassignable | ✅ `x.value = {...}` | ❌ loses reactivity |
| Destructure  | keep as ref          | breaks reactivity   |

**Key gotchas:**

- In the **template**, refs are **auto-unwrapped** — write `{{ count }}`, not `{{ count.value }}`.
- **Reassigning** a `reactive` object breaks reactivity: `state = {...}` ❌. A `ref` can be reassigned.
- **Destructuring** a `reactive` loses reactivity — use `toRefs()` to keep it:

```ts
const { count } = toRefs(state); // count is a ref, stays reactive
```

**Recommendation:** prefer **`ref`** as the default — it's consistent (works for everything, reassignable). Use `reactive` for grouped, related object state when you prefer property access.
