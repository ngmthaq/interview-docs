# 16. What is Dependency Injection (DI)? (Mid → Senior)

**Dependency Injection** means a class **receives its dependencies from outside** instead of creating them itself. It's the practical way to achieve the **Dependency Inversion Principle**.

```ts
interface Mailer {
  send(to: string, body: string): void;
}

// ❌ Without DI — hard-wired, can't swap or mock
class OrderServiceBad {
  private mailer = new SmtpMailer();
}

// ✅ With DI — dependency injected via constructor
class OrderService {
  constructor(private mailer: Mailer) {}
  placeOrder(email: string) {
    this.mailer.send(email, "Order confirmed");
  }
}

// Wire it up (or let a DI container do it)
const service = new OrderService(new SmtpMailer());
```

**Benefits:**

- **Testability** — inject a mock `Mailer` in tests.
- **Loose coupling** — depend on the interface, swap implementations freely.
- **Flexibility** — configuration decides concrete types.

**Types:** constructor injection (most common), setter injection, interface injection. Frameworks like NestJS/Spring provide DI **containers** to auto-wire dependencies.
