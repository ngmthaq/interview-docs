# 8. Explain the Adapter pattern. (Junior → Mid)

**Adapter** converts one interface into another that a client expects — letting **incompatible interfaces work together**. Think of a power plug adapter.

```ts
// Client expects this interface
interface Logger {
  log(message: string): void;
}

// Third-party lib with a different API we can't change
class ExternalLib {
  writeLine(text: string) {
    console.log(text);
  }
}

// Adapter bridges the gap
class ExternalLibAdapter implements Logger {
  constructor(private lib: ExternalLib) {}
  log(message: string) {
    this.lib.writeLine(message);
  }
}

const logger: Logger = new ExternalLibAdapter(new ExternalLib());
logger.log("works!");
```

**When to use:**

- Integrating a **third-party / legacy** API without changing your code.
- Making two systems with mismatched contracts cooperate.

**Key point:** the adapter _wraps_, it doesn't modify — the original class stays untouched.
