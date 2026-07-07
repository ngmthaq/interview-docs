# 14. How does OOP polymorphism compare to FP's higher-order functions? (Mid → Senior)

Both solve the same problem — **varying behavior without changing the caller** — but differently.

**OOP:** define an interface, pass different implementations (subtype polymorphism).

```ts
interface Discount {
  apply(price: number): number;
}
class Percent implements Discount {
  apply(p: number) {
    return p * 0.9;
  }
}

function checkout(d: Discount, price: number) {
  return d.apply(price);
}
```

**FP:** pass a **function** as an argument (higher-order function).

```ts
type Discount = (price: number) => number;
const percent: Discount = (p) => p * 0.9;

const checkout = (d: Discount, price: number) => d(price);
```

**Comparison:**

- OOP is better when a type carries **multiple related behaviors + state**.
- FP is lighter when you just need to **inject one behavior** — no class ceremony.
- The **Strategy pattern** in OOP is essentially "pass a function" done with objects.
