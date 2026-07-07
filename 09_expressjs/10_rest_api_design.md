# 10. How do you design a REST API in Express? (Junior)

A **RESTful** API models **resources** as URLs and uses **HTTP methods** for actions, returning appropriate **status codes**.

```ts
const router = Router();

router.get("/articles", list); // 200 — collection
router.post("/articles", create); // 201 — created
router.get("/articles/:id", getOne); // 200 / 404
router.put("/articles/:id", replace); // 200 — full update
router.patch("/articles/:id", update); // 200 — partial update
router.delete("/articles/:id", remove); // 204 — no content

app.use("/api/v1", router); // versioned base path
```

**Conventions:**

- **Nouns, not verbs** in URLs (`/articles`, not `/getArticles`).
- **Plural** resource names; nest for relationships (`/articles/:id/comments`).
- Correct **status codes**: 200, 201, 204, 400, 401, 403, 404, 409, 500.
- **Version** the API (`/api/v1`) and support pagination/filtering via query params.
- Return consistent **JSON error shapes**.

**Key point:** REST maps resources to URLs and actions to HTTP verbs with meaningful status codes — use plural nouns, version the base path, nest relationships, and keep response/error shapes consistent.
