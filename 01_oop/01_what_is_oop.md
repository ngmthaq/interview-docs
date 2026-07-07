# 1. What is OOP? (Fresher)

**Object-Oriented Programming** is a programming paradigm that organizes code around **objects** — units that bundle together **data (state)** and **behavior (methods)**.

Instead of thinking in terms of "functions that operate on data", you think in terms of "objects that own their data and know how to act on it".

```ts
class User {
  constructor(private name: string) {}

  greet() {
    return `Hi, I'm ${this.name}`;
  }
}
```

**Key point:** OOP is a _way of structuring code_, not a library or a design pattern.
