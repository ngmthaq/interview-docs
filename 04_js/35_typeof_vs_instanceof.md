# 35. typeof vs instanceof. (Junior)

Both check types, but at different levels.

**`typeof`** — returns a **string** for a value's primitive type. Best for primitives:

```js
typeof "hi"; // "string"
typeof 42; // "number"
typeof true; // "boolean"
typeof undefined; // "undefined"
typeof Symbol(); // "symbol"
typeof 10n; // "bigint"
typeof function () {}; // "function"
typeof {}; // "object"
typeof null; // "object"  ⚠️ historical bug
typeof []; // "object"  (can't distinguish arrays)
```

**`instanceof`** — checks whether an object's **prototype chain** contains a constructor's `prototype`. Best for objects/classes:

```js
[] instanceof Array; // true
[] instanceof Object; // true (Array extends Object)
new Date() instanceof Date; // true
class Dog {}
new Dog() instanceof Dog; // true
```

**Gotchas & better checks:**

- `typeof null === "object"` and `typeof [] === "object"` — use `Array.isArray(x)` for arrays and `x === null` for null.
- `instanceof` **fails across realms** (e.g. iframes/worker) since constructors differ; `Array.isArray` and `Object.prototype.toString.call(x)` are robust alternatives.

```js
Object.prototype.toString.call([]); // "[object Array]"
```

**Key point:** use `typeof` for primitives (mind `null`/arrays reporting `"object"`) and `instanceof` for class/prototype checks (mind cross-realm failures); reach for `Array.isArray` or `Object.prototype.toString.call()` when you need reliable object-type detection.
