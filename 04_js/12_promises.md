# 12. What is a Promise? (Junior → Mid)

A **Promise** represents the eventual result of an async operation. It has three states: **pending → fulfilled** or **rejected**.

```js
const p = new Promise((resolve, reject) => {
  setTimeout(() => resolve("done"), 1000);
});

p.then((result) => console.log(result)) // handle success
  .catch((err) => console.error(err)) // handle failure
  .finally(() => console.log("cleanup")); // always runs
```

**Chaining** avoids callback hell — each `.then` returns a new promise:

```js
login(user)
  .then((u) => getProfile(u))
  .then((p) => getPosts(p))
  .catch((err) => console.error(err)); // one place for errors
```

**Combinators:**

```js
Promise.all([a, b, c]); // waits for all; rejects if any fails
Promise.allSettled([a, b]); // waits for all, never short-circuits
Promise.race([a, b]); // first to settle (resolve or reject)
Promise.any([a, b]); // first to fulfill
```

**Key point:** Promises flatten async code and centralize error handling. They're the foundation async/await builds on.
