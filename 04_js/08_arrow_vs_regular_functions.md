# 8. Arrow functions vs regular functions? (Junior → Mid)

| Feature                       | Regular function    | Arrow function              |
| ----------------------------- | ------------------- | --------------------------- |
| `this`                        | Dynamic (call site) | Lexical (surrounding scope) |
| `arguments` object            | Yes                 | No                          |
| Usable as constructor (`new`) | Yes                 | No                          |
| Hoisted (as declaration)      | Yes                 | No (assigned to a var)      |
| Good for methods              | Yes                 | Often no (no own `this`)    |

```js
const obj = {
  value: 10,
  regular() {
    return this.value;
  }, // 10
  arrow: () => this.value, // undefined — `this` is outer scope
};
```

**Arrows shine in callbacks** where you want to keep the outer `this`:

```js
class Timer {
  seconds = 0;
  start() {
    setInterval(() => this.seconds++, 1000); // arrow keeps `this` = instance
  }
}
```

**Rest instead of `arguments`:**

```js
const sum = (...nums) => nums.reduce((a, b) => a + b, 0);
```

**Key point:** use arrows for callbacks and short functions; use regular functions for object methods and when you need `this`, `arguments`, or `new`.
