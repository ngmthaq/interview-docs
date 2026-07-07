# 11. OOP vs Functional Programming — what's the core difference? (Junior → Mid)

Both are paradigms for organizing code, but they optimize for different things.

| Aspect          | OOP                              | Functional Programming (FP)             |
| --------------- | -------------------------------- | --------------------------------------- |
| Core unit       | Objects (state + behavior)       | Functions (pure transformations)        |
| State           | Mutable, encapsulated in objects | Immutable, passed explicitly            |
| Data & behavior | Bundled together                 | Kept separate                           |
| Flow            | Objects sending messages         | Data piped through functions            |
| Reuse           | Inheritance / composition        | Function composition / higher-order fns |

```ts
// OOP: object owns state and behavior
class Counter {
  private count = 0;
  increment() {
    this.count++;
  }
}

// FP: data in, new data out, no mutation
const increment = (count: number) => count + 1;
```

**One-liner:** OOP models the world as _objects that change_; FP models it as _data being transformed by functions_.
