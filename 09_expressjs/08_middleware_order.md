# 8. Why does middleware order matter? (Junior)

Express executes middleware **top to bottom in registration order**. A misplaced middleware runs too early or too late — a common source of bugs.

```ts
// CORRECT ordering
app.use(express.json()); // 1. parse body first
app.use(morgan("dev")); // 2. log requests
app.use("/api", authGuard); // 3. auth before protected routes
app.use("/api", apiRouter); // 4. handle the routes
app.use(notFoundHandler); // 5. 404 for unmatched paths
app.use(errorHandler); // 6. errors LAST (4-arg)
```

**Consequences of wrong order:**

- Body parser **after** the route → `req.body` is `undefined`.
- Auth guard **after** the route → the handler runs unauthenticated.
- Error handler **before** routes → it never catches their errors.
- 404 handler **before** routes → everything returns 404.

**Rule of thumb:** parsers & security first → logging → routes → 404 → error handler last.

**Key point:** middleware runs in registration order, so place parsers/security/logging before routes, and the 404 and error handlers last — most "why is `req.body` empty / auth skipped" bugs are ordering mistakes.
