# 1. What is a design pattern? (Fresher)

A **design pattern** is a **reusable, proven solution to a common software design problem**. It's not code you copy-paste — it's a _template_ or _approach_ you adapt to your situation.

Patterns give teams a **shared vocabulary**: saying "let's use a Factory here" instantly communicates intent.

```ts
// "Factory" — the caller doesn't use `new` directly
function createLogger(env: string) {
  return env === "prod" ? new FileLogger() : new ConsoleLogger();
}
```

**Key points:**

- Patterns are **language-agnostic ideas**, built on top of OOP principles.
- They come from the "Gang of Four" (GoF) book, which cataloged 23 classic patterns.
- A pattern is a **guideline, not a rule** — use it only when it genuinely simplifies the design.
