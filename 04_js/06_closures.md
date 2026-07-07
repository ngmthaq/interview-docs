# 6. What is a closure? (Junior → Mid)

A **closure** is a function that **remembers variables from its outer scope** even after that outer function has returned.

```js
function counter() {
  let count = 0; // private state
  return function () {
    count++; // closes over `count`
    return count;
  };
}

const inc = counter();
inc(); // 1
inc(); // 2 — `count` persists between calls
```

**Why it works:** the inner function keeps a reference to its lexical environment, so `count` isn't garbage-collected.

**Practical uses:**

- **Data privacy** — emulate private variables (module pattern).
- **Function factories** — `multiplyBy(2)`.
- **Callbacks / event handlers** that need surrounding state.

**Classic gotcha:**

```js
for (var i = 0; i < 3; i++) setTimeout(() => console.log(i)); // 3,3,3
for (let i = 0; i < 3; i++) setTimeout(() => console.log(i)); // 0,1,2
```

`let` creates a new binding per iteration; `var` shares one.
