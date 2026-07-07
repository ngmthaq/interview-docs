# 9. Explain the Decorator pattern. (Mid)

**Decorator** adds behavior to an object **dynamically** by wrapping it, without changing its class or affecting other instances. A flexible alternative to subclassing.

```ts
interface Coffee {
  cost(): number;
}

class BasicCoffee implements Coffee {
  cost() {
    return 2;
  }
}

// Decorators wrap a Coffee and add to it
class MilkDecorator implements Coffee {
  constructor(private coffee: Coffee) {}
  cost() {
    return this.coffee.cost() + 0.5;
  }
}
class SugarDecorator implements Coffee {
  constructor(private coffee: Coffee) {}
  cost() {
    return this.coffee.cost() + 0.2;
  }
}

let order: Coffee = new BasicCoffee();
order = new MilkDecorator(order);
order = new SugarDecorator(order);
order.cost(); // 2.7
```

**Benefits:**

- Stack features in any combination without a class explosion (`MilkSugarCoffee`, etc.).
- Follows Open/Closed — extend behavior without modifying `BasicCoffee`.

Real-world: HTTP middleware, stream wrappers, React HOCs are decorator-style.
