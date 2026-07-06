# 15. When would you choose OOP over FP, and vice versa? (Senior)

A senior answer avoids dogma — the paradigms are complementary, not rivals.

**Reach for OOP when:**
- Modeling a **domain with clear entities** that own state and lifecycle (User, Order, Account).
- Building **stateful systems** with well-defined boundaries (services, aggregates).
- You benefit from encapsulation to protect **invariants**.

**Reach for FP when:**
- **Transforming data** through pipelines (map/filter/reduce, ETL, stream processing).
- You need **concurrency / parallelism** — immutability removes whole classes of bugs.
- Logic should be **pure and easily testable** (business rules, calculations).

**The real-world answer — multi-paradigm:**
```ts
// OOP for the boundary / entity...
class OrderService {
  constructor(private repo: OrderRepo) {}

  // ...FP for the pure logic inside
  totalWithTax(items: Item[]) {
    return items
      .map(i => i.price)
      .reduce((sum, p) => sum + p, 0) * 1.1;
  }
}
```

**Key point:** Most modern languages (TypeScript, Kotlin, Scala, C#) are multi-paradigm on purpose. Use **OOP to structure the system** and **FP to write the logic**. Choose per problem, not per ideology.
