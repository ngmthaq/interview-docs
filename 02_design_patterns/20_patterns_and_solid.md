# 20. How do design patterns relate to SOLID principles? (Senior)

Design patterns are **concrete techniques**; SOLID are the **principles** they help you honor. Most patterns exist precisely to satisfy one or more SOLID rules.

| Pattern              | Principle it serves             | How                                                     |
| -------------------- | ------------------------------- | ------------------------------------------------------- |
| Strategy / Factory   | **O**pen/Closed                 | Add new behavior via new classes, not edits             |
| Adapter              | **D**ependency Inversion        | Depend on an interface, adapt the concrete              |
| Decorator            | **O**pen/Closed + **S**RP       | Extend behavior by composition, one concern per wrapper |
| Observer             | **O**pen/Closed                 | Add subscribers without changing the subject            |
| Dependency Injection | **D**ependency Inversion        | Depend on abstractions, inject concretions              |
| Facade / Repository  | **S**RP + Interface Segregation | Narrow, focused interfaces over complex subsystems      |

```ts
// Strategy satisfies Open/Closed: new pricing = new class, Checkout untouched
interface PricingStrategy {
  getPrice(base: number): number;
}
```

**Interview framing:**

- SOLID tells you **what "good design" means**.
- Patterns are **battle-tested ways to get there**.
- But the goal is the _principle_, not the pattern — a simple function can satisfy Open/Closed without any named pattern. Reach for a pattern only when it makes the SOLID goal easier, not as a checkbox.
