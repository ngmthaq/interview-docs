# 11. How do you handle async route handlers? (Mid)

In **Express 4**, if a `Promise` rejects inside an `async` handler and you don't catch it, Express **won't** catch it — the request hangs and the error is unhandled.

```ts
// BROKEN in Express 4 — rejection is not forwarded
app.get("/user", async (req, res) => {
  const user = await db.findUser(req.query.id); // if this throws → hang
  res.json(user);
});
```

**Solutions:**

**1. try/catch + next(err):**

```ts
app.get("/user", async (req, res, next) => {
  try {
    res.json(await db.findUser(req.query.id));
  } catch (err) {
    next(err);
  }
});
```

**2. A wrapper** to avoid repeating try/catch:

```ts
const asyncHandler = (fn) => (req, res, next) => Promise.resolve(fn(req, res, next)).catch(next);

app.get(
  "/user",
  asyncHandler(async (req, res) => {
    res.json(await db.findUser(req.query.id));
  }),
);
```

**3. Express 5** — forwards rejected promises to error middleware automatically. Or use `express-async-errors`.

**Key point:** Express 4 ignores async rejections, so wrap handlers in try/catch + `next(err)` or an `asyncHandler` helper; Express 5 (and `express-async-errors`) forward them automatically.
