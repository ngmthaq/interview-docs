# 15. What is a higher-order function? (Junior)

A **higher-order function (HOF)** either **takes a function as an argument**, **returns a function**, or both.

```js
// Takes a function
[1, 2, 3].map((x) => x * 2); // [2, 4, 6]

// Returns a function
function multiplier(factor) {
  return (x) => x * factor;
}
const double = multiplier(2);
double(5); // 10
```

**Why they matter:**

- Enable **abstraction and reuse** — pass behavior as data.
- Foundation of functional programming (`map`, `filter`, `reduce`).
- Power patterns like middleware, decorators, and callbacks.

**Real example — a logging wrapper:**

```js
function withLogging(fn) {
  return (...args) => {
    console.log("calling with", args);
    return fn(...args);
  };
}
const add = withLogging((a, b) => a + b);
add(2, 3); // logs, then returns 5
```

**Key point:** functions are **first-class citizens** in JS — they can be stored, passed, and returned like any value, which is what makes HOFs possible.
