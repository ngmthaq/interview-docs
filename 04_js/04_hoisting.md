# 4. What is hoisting? (Fresher → Junior)

**Hoisting** is JavaScript moving **declarations** to the top of their scope during compilation, before code runs.

```js
console.log(x); // undefined (declaration hoisted, not the value)
var x = 5;

// interpreted as:
var x;
console.log(x); // undefined
x = 5;
```

**Functions vs variables:**

```js
sayHi(); // ✅ works — function declarations fully hoisted
function sayHi() {
  return "hi";
}

sayBye(); // ❌ TypeError: not a function
var sayBye = function () {}; // only `var sayBye` hoisted (= undefined)
```

**`let` / `const` — Temporal Dead Zone (TDZ):**

```js
console.log(y); // ReferenceError (in TDZ, not undefined)
let y = 10;
```

**Key point:** `var` is hoisted and initialized to `undefined`; `let`/`const` are hoisted but stay in the TDZ until declared; function **declarations** are hoisted entirely.
