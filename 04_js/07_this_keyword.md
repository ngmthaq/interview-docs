# 7. How does `this` work in JavaScript? (Mid)

`this` is determined by **how a function is called**, not where it's defined.

| Call style              | `this` refers to                           |
| ----------------------- | ------------------------------------------ |
| Method call `obj.fn()`  | `obj`                                      |
| Plain call `fn()`       | `undefined` (strict) / global              |
| Constructor `new Fn()`  | the new instance                           |
| `fn.call/apply/bind(x)` | `x`                                        |
| Arrow function          | inherited from surrounding scope (lexical) |

```js
const user = {
  name: "Ann",
  greet() {
    return `Hi ${this.name}`;
  },
};
user.greet(); // 'Hi Ann'

const g = user.greet;
g(); // 'Hi undefined' — lost context
```

**Arrow functions don't have their own `this`:**

```js
const obj = {
  items: [1, 2],
  log() {
    this.items.forEach(() => console.log(this.items)); // ✅ arrow keeps `this`
  },
};
```

**Key point:** regular functions get `this` from the **call site**; arrow functions capture `this` **lexically** — ideal for callbacks.
