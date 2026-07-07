# 11. What is a callback, and what is callback hell? (Junior)

A **callback** is a function passed as an argument to be **called later** — the basis of async programming.

```js
function fetchData(cb) {
  setTimeout(() => cb("data"), 1000);
}
fetchData((result) => console.log(result)); // 'data' after 1s
```

**Callback hell** — deeply nested callbacks for sequential async steps, hard to read and maintain:

```js
login(user, (err, u) => {
  getProfile(u, (err, p) => {
    getPosts(p, (err, posts) => {
      // "pyramid of doom" — deep nesting, tangled error handling
    });
  });
});
```

**Problems:** hard to read, error handling repeated at every level, difficult to reason about.

**Fixes:**

- **Promises** with `.then()` chaining (flattens nesting).
- **async/await** for synchronous-looking async code.

**Key point:** callbacks are fundamental, but for sequential async logic prefer Promises / async-await to avoid the pyramid of doom.
