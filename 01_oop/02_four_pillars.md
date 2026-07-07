# 2. What are the 4 pillars of OOP? (Fresher)

| Pillar            | Meaning                                       |
| ----------------- | --------------------------------------------- |
| **Encapsulation** | Hide internal state; expose controlled access |
| **Abstraction**   | Expose _what_ an object does, hide _how_      |
| **Inheritance**   | Reuse behavior by extending a base class      |
| **Polymorphism**  | One interface, many implementations           |

```ts
// Encapsulation
class Account {
  private balance = 0;
  deposit(amount: number) {
    if (amount <= 0) throw new Error("Invalid amount");
    this.balance += amount;
  }
}
```

**Tip:** In an interview, always give a one-line example per pillar — don't just list them.
