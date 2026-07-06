# 12. How do OOP and FP handle state and mutability? (Mid)

**OOP** — state lives *inside* objects and is usually **mutable**. Methods change the object's internal state over time.

```ts
class Cart {
  private items: string[] = [];
  add(item: string) { this.items.push(item); } // mutates state
}
```

**FP** — data is **immutable**. You never modify; you produce a **new value**.

```ts
const addItem = (items: readonly string[], item: string) => [...items, item]; // new array
```

**Why it matters:**
- Immutability makes code **easier to reason about** — a value never changes under you.
- It makes **concurrency safer** — no shared mutable state, no race conditions.
- OOP's mutable state can be more intuitive for modeling real-world entities, but needs discipline (encapsulation) to stay safe.
