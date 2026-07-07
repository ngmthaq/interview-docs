# 5. Factory Method vs Abstract Factory? (Mid)

- **Factory Method** creates **one product**.
- **Abstract Factory** creates **families of related products** that are meant to be used together.

```ts
interface Button {
  render(): void;
}
interface Checkbox {
  render(): void;
}

// A factory that produces a whole matching UI family
interface UIFactory {
  createButton(): Button;
  createCheckbox(): Checkbox;
}

class DarkUIFactory implements UIFactory {
  createButton() {
    return new DarkButton();
  }
  createCheckbox() {
    return new DarkCheckbox();
  }
}
class LightUIFactory implements UIFactory {
  createButton() {
    return new LightButton();
  }
  createCheckbox() {
    return new LightCheckbox();
  }
}
```

**Key point:** Abstract Factory guarantees **consistency** — you can't accidentally mix a dark button with a light checkbox. Use it when products come in coordinated sets (themes, cross-platform widgets, DB drivers).
