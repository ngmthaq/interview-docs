# 14. Explain the Strategy pattern. (Junior → Mid)

**Strategy** defines a family of **interchangeable algorithms**, encapsulates each one, and lets you swap them at runtime. It replaces sprawling `if/else` or `switch` blocks.

```ts
interface PricingStrategy {
  getPrice(base: number): number;
}

class RegularPricing implements PricingStrategy {
  getPrice(base: number) {
    return base;
  }
}
class MemberPricing implements PricingStrategy {
  getPrice(base: number) {
    return base * 0.8;
  }
}

class Checkout {
  constructor(private strategy: PricingStrategy) {}
  setStrategy(s: PricingStrategy) {
    this.strategy = s;
  }
  total(base: number) {
    return this.strategy.getPrice(base);
  }
}

const checkout = new Checkout(new MemberPricing());
checkout.total(100); // 80
```

**Benefits:**

- Add a new algorithm without touching existing code (Open/Closed).
- Swap behavior at runtime.

**Note:** in FP/JS, a strategy is often just a **function passed as an argument** — same idea, less ceremony.
