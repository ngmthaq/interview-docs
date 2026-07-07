# 4. Explain the Factory Method pattern. (Junior)

**Factory Method** moves object creation behind a method so callers don't depend on concrete classes. You ask for _what_ you want; the factory decides _which_ class to build.

```ts
interface Notifier {
  send(msg: string): void;
}

class EmailNotifier implements Notifier {
  send(msg: string) {
    console.log("Email:", msg);
  }
}
class SmsNotifier implements Notifier {
  send(msg: string) {
    console.log("SMS:", msg);
  }
}

function createNotifier(channel: "email" | "sms"): Notifier {
  return channel === "email" ? new EmailNotifier() : new SmsNotifier();
}
```

**Benefits:**

- Callers depend on the **interface**, not concrete types (loose coupling).
- Adding a new type = add a class + one branch, callers unchanged (Open/Closed).
- Centralizes construction logic in one place.
