# 19. What are anti-patterns, and when do design patterns hurt? (Senior)

An **anti-pattern** is a common "solution" that looks helpful but creates more problems than it solves.

**Common anti-patterns:**

- **God Object** — one class that does everything (violates SRP).
- **Spaghetti code** — no structure, tangled control flow.
- **Golden Hammer** — forcing one favorite pattern onto every problem.
- **Premature abstraction** — layers/interfaces added "just in case", never used.

**When patterns hurt:**

```ts
// Overkill: a Factory + Strategy + interface for a value that never changes
interface Greeter {
  greet(): string;
}
class EnglishGreeter implements Greeter {
  greet() {
    return "Hi";
  }
}
class GreeterFactory {
  static create(): Greeter {
    return new EnglishGreeter();
  }
}
// ...when `const greet = () => 'Hi'` was enough
```

**Senior takeaway:**

- Patterns add **indirection** — that's a cost, not free.
- Apply a pattern when the problem it solves **actually exists** (repeated change, real variation), not preemptively.
- **YAGNI** ("You Aren't Gonna Need It") — prefer the simplest thing that works; refactor to a pattern when pain appears.
