# 24. What is currying and partial application? (Senior)

**Currying** transforms a function of N arguments into a chain of N functions each taking **one argument**.

```js
// Normal
const add = (a, b, c) => a + b + c;
add(1, 2, 3); // 6

// Curried
const addC = (a) => (b) => (c) => a + b + c;
addC(1)(2)(3); // 6
```

**Partial application** — fix some arguments now, supply the rest later.

```js
const multiply = (a, b) => a * b;
const double = multiply.bind(null, 2); // fix a = 2
double(5); // 10
```

**A generic curry:**

```js
function curry(fn) {
  return function curried(...args) {
    return args.length >= fn.length ? fn(...args) : (...next) => curried(...args, ...next);
  };
}
const sum = curry((a, b, c) => a + b + c);
sum(1)(2)(3);
sum(1, 2)(3);
sum(1)(2, 3); // all 6
```

**Why it's useful:**

- Build **specialized functions** from general ones (`addTax = applyRate(0.1)`).
- Enables clean **function composition** and reusable pipelines.

**Key point:** currying = one arg at a time; partial application = pre-fill some args. Both create reusable, configured functions.
