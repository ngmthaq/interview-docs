# 8. What is coupling and cohesion? How do you keep coupling low? (Mid → Senior)

- **Coupling** = how dependent modules are on each other. **Want it LOW.**
- **Cohesion** = how focused a module is on a single responsibility. **Want it HIGH.**

**Tight coupling (bad):**
```ts
class OrderService {
  private mailer = new SmtpMailer(); // hard-wired dependency
}
```

**Loose coupling (good) — via dependency injection + interface:**
```ts
interface Mailer { send(to: string, body: string): void; }

class OrderService {
  constructor(private mailer: Mailer) {} // injected, swappable
}
```

**Techniques to reduce coupling:** program to interfaces, dependency injection, and keeping each class single-purpose (SRP).
