# 7. How do you handle errors in Express? (Junior)

Express recognizes **error-handling middleware** by its **four arguments** `(err, req, res, next)`. Errors passed via `next(err)` skip normal middleware and jump straight to it.

```ts
// A route that forwards an error
app.get("/users/:id", async (req, res, next) => {
  try {
    const user = await findUser(req.params.id);
    if (!user) return next(new NotFoundError("User not found"));
    res.json(user);
  } catch (err) {
    next(err); // forward to the error handler
  }
});

// Centralized error handler — register LAST
app.use((err, req, res, next) => {
  const status = err.status ?? 500;
  res.status(status).json({ error: err.message });
});
```

**Key rules:**

- Error middleware must have **exactly 4 params** and be registered **after** all routes.
- In **Express 4**, errors thrown in **async** handlers are NOT caught automatically — you must `try/catch` and call `next(err)` (or use a wrapper). **Express 5** forwards rejected promises automatically.
- Use a custom `AppError` class carrying a `status` for consistent responses.

**Key point:** centralize error handling in a 4-arg `(err, req, res, next)` middleware registered last; forward errors with `next(err)`, and remember Express 4 needs manual `try/catch` for async handlers (Express 5 handles it).
