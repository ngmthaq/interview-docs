# 5. Composition vs Inheritance — which do you prefer and why? (Junior → Mid)

**Inheritance** ("is-a"): `Dog extends Animal`.
**Composition** ("has-a"): `Car has an Engine`.

**Prefer composition** in most cases because inheritance creates tight coupling and fragile hierarchies.

```ts
// Composition
class Engine {
  start() { return 'engine on'; }
}

class Car {
  constructor(private engine: Engine) {}
  start() { return this.engine.start(); }
}
```

**Why composition wins:**
- More flexible — swap behavior at runtime
- Avoids deep, rigid class trees
- Easier to test (inject mocks)

Rule of thumb: **"Favor composition over inheritance."**
