# 2. How does routing work in Express? (Fresher)

**Routing** maps an incoming HTTP **method + URL path** to a handler function.

```ts
app.get("/users", (req, res) => res.json(users)); // list
app.post("/users", (req, res) => res.status(201).json(created)); // create
app.get("/users/:id", (req, res) => res.json(byId(req.params.id))); // read one
app.put("/users/:id", (req, res) => res.json(updated)); // replace
app.delete("/users/:id", (req, res) => res.status(204).end()); // delete
```

**Route features:**

- **Route params** — `:id` captured in `req.params`.
- **Query strings** — `/search?q=node` read from `req.query`.
- **Multiple handlers** — pass middleware before the final handler: `app.get("/x", auth, handler)`.
- **`app.all`** / **`app.route()`** — match any method or chain handlers for one path.

```ts
app.route("/books").get(listBooks).post(createBook);
```

**Key point:** routing binds an HTTP method and path pattern to handlers; dynamic segments (`:id`) land in `req.params` and query strings in `req.query`, and you can chain middleware before the handler.
