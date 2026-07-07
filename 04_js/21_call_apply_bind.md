# 21. call, apply, and bind? (Mid)

All three set `this` explicitly for a function; they differ in how they pass arguments and when they run.

```js
function greet(greeting, punc) {
  return `${greeting}, ${this.name}${punc}`;
}
const user = { name: "Ann" };

// call — invoke now, args listed individually
greet.call(user, "Hi", "!"); // 'Hi, Ann!'

// apply — invoke now, args as an array
greet.apply(user, ["Hey", "."]); // 'Hey, Ann.'

// bind — returns a NEW function with `this` fixed (call later)
const bound = greet.bind(user);
bound("Hello", "?"); // 'Hello, Ann?'
```

| Method  | Invokes?       | Args                         |
| ------- | -------------- | ---------------------------- |
| `call`  | Now            | Comma-separated              |
| `apply` | Now            | Array                        |
| `bind`  | Returns new fn | Comma-separated (partial ok) |

**Common use — fix `this` for a callback:**

```js
button.addEventListener("click", this.handleClick.bind(this));
```

**Key point:** `call`/`apply` invoke immediately (differ only in arg format); `bind` returns a reusable function with `this` permanently set.
