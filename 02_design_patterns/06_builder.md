# 6. Explain the Builder pattern. (Mid)

**Builder** constructs a complex object **step by step**, avoiding a giant constructor with many parameters ("telescoping constructor" problem).

```ts
class Pizza {
  size = "M";
  toppings: string[] = [];
  cheese = false;
}

class PizzaBuilder {
  private pizza = new Pizza();

  setSize(s: string) {
    this.pizza.size = s;
    return this;
  }
  addTopping(t: string) {
    this.pizza.toppings.push(t);
    return this;
  }
  withCheese() {
    this.pizza.cheese = true;
    return this;
  }
  build() {
    return this.pizza;
  }
}

const pizza = new PizzaBuilder().setSize("L").addTopping("mushroom").withCheese().build();
```

**Benefits:**

- Readable, **fluent** construction (method chaining via `return this`).
- Handles **optional** parameters cleanly.
- Can enforce validation in `build()` before returning a valid object.
