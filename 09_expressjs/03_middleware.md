# 3. What is middleware in Express? (Fresher)

**Middleware** are functions that run **in sequence** during the request/response cycle. Each receives `(req, res, next)` and either passes control with `next()` or ends the response.

```ts
// Application-level middleware — runs for every request
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next(); // pass to the next middleware
});
```

**Types of middleware:**

- **Application-level** — `app.use(...)` / `app.get(...)`.
- **Router-level** — bound to an `express.Router()` instance.
- **Built-in** — `express.json()`, `express.static()`, `express.urlencoded()`.
- **Third-party** — `cors`, `helmet`, `morgan`.
- **Error-handling** — special 4-arg signature `(err, req, res, next)`.

**The `next()` function** is the key: call it to continue, call `next(err)` to jump to error handling, or send a response to stop the chain.

**Key point:** middleware is the heart of Express — a chain of `(req, res, next)` functions for cross-cutting logic (logging, auth, parsing, errors); registration order defines execution order, and `next()` controls flow.
