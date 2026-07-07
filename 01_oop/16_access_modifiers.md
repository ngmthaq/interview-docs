# 16. What are access modifiers and why do they matter? (Junior)

Access modifiers control **who can see and use** a class member. They are how encapsulation is enforced.

| Modifier    | Accessible from                  |
| ----------- | -------------------------------- |
| `public`    | Anywhere (default)               |
| `protected` | The class **and** its subclasses |
| `private`   | Only inside the same class       |

```ts
class Account {
  public owner: string; // anyone
  protected type = "savings"; // this class + subclasses
  private balance = 0; // this class only

  constructor(owner: string) {
    this.owner = owner;
  }

  deposit(amount: number) {
    this.balance += amount;
  } // controlled access
}
```

**Why it matters:** by making state `private` and exposing only intentional methods, the object protects its **invariants** — outside code can't put it into an invalid state.

> Note: TypeScript's `private` is compile-time only. For true runtime privacy in JS, use `#field` (ECMAScript private fields).
