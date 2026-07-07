# 23. null vs undefined? (Fresher)

- **`undefined`** — a variable declared but **not assigned**; the "default empty" set by JS.
- **`null`** — an **intentional** "no value", set by the developer.

```js
let a; // undefined (not assigned)
let b = null; // null (deliberately empty)

const obj = {};
obj.missing; // undefined (property doesn't exist)

function fn(x) {
  return x;
}
fn(); // undefined (missing argument)
```

**Comparisons:**

```js
null == undefined; // true  (loose — both "empty")
null === undefined; // false (different types)

typeof undefined; // 'undefined'
typeof null; // 'object'  ← historical bug
```

**Nullish handling:**

```js
const val = input ?? "default"; // uses default only for null/undefined (not '' or 0)
user?.address?.city; // optional chaining — undefined if any link missing
```

**Key point:** `undefined` = "not set yet (by the engine)"; `null` = "intentionally empty (by you)". Use `??` and `?.` to handle both safely.
