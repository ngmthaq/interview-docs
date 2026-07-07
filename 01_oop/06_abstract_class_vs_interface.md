# 6. What is an abstract class vs an interface? (Mid)

|                         | Abstract class            | Interface                      |
| ----------------------- | ------------------------- | ------------------------------ |
| Can have implementation | Yes (partial)             | No (contract only)             |
| Fields / state          | Yes                       | No (in most languages)         |
| Multiple inheritance    | No                        | Yes (implement many)           |
| Use when                | Sharing common base logic | Defining a capability/contract |

```ts
interface Payable {
  pay(amount: number): void;
}

abstract class BasePayment implements Payable {
  abstract pay(amount: number): void;
  protected log(msg: string) {
    console.log(msg);
  } // shared logic
}
```

**Rule:** Use an **interface** to define _what_ something can do; use an **abstract class** when subclasses _share real implementation_.
