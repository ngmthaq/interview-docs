# 13. Explain async/await. (Mid)

`async/await` is syntactic sugar over Promises that lets you write async code that **reads like synchronous code**.

```js
async function loadUser(id) {
  try {
    const user = await getUser(id); // pauses until promise resolves
    const posts = await getPosts(user); // sequential
    return { user, posts };
  } catch (err) {
    console.error(err); // handles any rejection
  }
}
```

- An `async` function **always returns a Promise**.
- `await` pauses the function until the promise settles (doesn't block the thread).
- Use `try/catch` for error handling (replaces `.catch`).

**Run in parallel when independent:**

```js
// ❌ Sequential — slow (waits one, then the other)
const a = await taskA();
const b = await taskB();

// ✅ Parallel — start both, then await
const [a, b] = await Promise.all([taskA(), taskB()]);
```

**Key point:** async/await improves readability, but you must still use `Promise.all` for concurrency — sequential `await`s run one at a time.
