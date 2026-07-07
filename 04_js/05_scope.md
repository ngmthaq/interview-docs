# 5. Explain scope in JavaScript. (Junior)

**Scope** determines where variables are accessible.

- **Global scope** — declared outside any function; available everywhere.
- **Function scope** — variables live only inside the function.
- **Block scope** — `let`/`const` inside `{}` (if, for, blocks).

```js
const g = "global";

function outer() {
  const f = "function";
  if (true) {
    let b = "block";
    console.log(g, f, b); // all visible
  }
  console.log(b); // ❌ ReferenceError — block-scoped
}
```

**Scope chain / lexical scope:** inner functions can access variables of outer functions, walking outward until global.

```js
function outer() {
  const x = 1;
  function inner() {
    return x;
  } // finds x in outer scope
  return inner();
}
```

**Key point:** JavaScript uses **lexical (static) scope** — scope is determined by _where code is written_, not where it's called.
