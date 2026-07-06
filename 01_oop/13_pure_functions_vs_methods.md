# 13. Pure functions vs object methods — what's the practical difference? (Mid)

A **pure function**:
1. Returns the same output for the same input.
2. Has **no side effects** (doesn't mutate external state, no I/O).

```ts
// Pure: depends only on inputs, changes nothing outside
const total = (prices: number[]) => prices.reduce((a, b) => a + b, 0);
```

An **object method** often depends on and mutates the object's internal state — the same call can return different results over time.

```ts
class Wallet {
  private balance = 0;
  spend(amount: number) { this.balance -= amount; return this.balance; } // impure
}
```

**Trade-off:**
- Pure functions are **trivial to test** (no setup, no mocks) and **cacheable/memoizable**.
- Methods are natural when behavior genuinely belongs to a stateful entity.
- Good practice: keep a **pure core** (business logic) and push side effects to the edges — even inside OOP code.
