# 3. What are JavaScript's data types? (Fresher)

**7 primitives** (immutable, compared by value):
`string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`.

**Non-primitive:** `object` (includes arrays, functions, dates).

```js
typeof "hi"; // 'string'
typeof 42; // 'number'
typeof true; // 'boolean'
typeof undefined; // 'undefined'
typeof null; // 'object'  ← historical bug
typeof Symbol(); // 'symbol'
typeof 10n; // 'bigint'
typeof {}; // 'object'
typeof []; // 'object'  (use Array.isArray to detect arrays)
typeof function () {}; // 'function'
```

**Primitive vs reference (key interview point):**

```js
let a = 1;
let b = a;
b = 2; // a is still 1 (copied by value)

let x = { n: 1 };
let y = x;
y.n = 2;
console.log(x.n); // 2 — objects copied by reference
```

**Key point:** primitives are copied by value; objects/arrays/functions are copied by **reference**.
