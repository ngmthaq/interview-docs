# 4. Difference between Overloading and Overriding? (Junior)

- **Overriding**: a subclass replaces a method inherited from its parent (runtime polymorphism).
- **Overloading**: multiple methods with the same name but different parameters (compile-time / signature-based).

```ts
class Animal {
  speak() {
    return "some sound";
  }
}

class Dog extends Animal {
  speak() {
    return "Woof";
  } // overriding
}
```

> TypeScript / JavaScript don't support true overloading like Java; you emulate it with optional params or union types.
