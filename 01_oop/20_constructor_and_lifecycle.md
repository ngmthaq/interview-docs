# 20. What is a constructor, and how is an object created? (Junior → Mid)

A **constructor** is a special method that runs when an object is created with `new`. Its job is to **initialize state** and enforce that the object starts in a valid state.

```ts
class Order {
  constructor(private items: string[]) {
    if (items.length === 0) {
      throw new Error('Order must have at least one item');
    }
  }
}
```

**What `new` actually does (JS):**
1. Creates a fresh empty object.
2. Links its prototype to the class's prototype.
3. Runs the constructor with `this` bound to the new object.
4. Returns the object (unless the constructor returns its own object).

**Related patterns:**
- **`super(...)`** — a subclass constructor must call the parent's constructor first.
- **Factory method** — a `static` method that builds and returns an instance, useful when construction is complex or needs a meaningful name (`User.fromJSON(...)`).

**Key point:** a constructor should validate inputs and set up invariants — not do heavy work like I/O (that hurts testability).
