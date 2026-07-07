# 1. var vs let vs const? (Fresher)

|            | `var`                | `let`        | `const`      |
| ---------- | -------------------- | ------------ | ------------ |
| Scope      | Function             | Block        | Block        |
| Re-assign  | Yes                  | Yes          | No           |
| Re-declare | Yes                  | No           | No           |
| Hoisting   | Hoisted, `undefined` | Hoisted, TDZ | Hoisted, TDZ |

```js
function demo() {
  if (true) {
    var a = 1; // function-scoped — leaks out of the block
    let b = 2; // block-scoped
    const c = 3; // block-scoped, can't reassign
  }
  console.log(a); // 1
  console.log(b); // ReferenceError
}
```

**`const` with objects:** the _binding_ is constant, but the object's contents can change:

```js
const user = { name: "A" };
user.name = "B"; // ✅ allowed
user = {}; // ❌ TypeError
```

**Rule:** default to `const`, use `let` when you must reassign, avoid `var`.
