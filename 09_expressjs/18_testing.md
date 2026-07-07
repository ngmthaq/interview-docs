# 18. How do you test an Express app? (Senior)

Test HTTP endpoints without spinning up a real network server using **`supertest`**, which drives the Express `app` in-process.

```ts
// app.ts must export the app WITHOUT calling app.listen()
import request from "supertest";
import app from "../app";

describe("Users API", () => {
  test("GET /users returns 200 + list", async () => {
    const res = await request(app).get("/users");
    expect(res.status).toBe(200);
    expect(Array.isArray(res.body)).toBe(true);
  });

  test("POST /users validates input", async () => {
    const res = await request(app).post("/users").send({ email: "bad" });
    expect(res.status).toBe(400);
  });
});
```

**Strategy:**

- **Unit** — test services/controllers with mocked repositories.
- **Integration** — test routes + middleware + real (or test) DB via supertest.
- Keep `app` and `server` **separate** so tests import `app` without opening a port.
- Use a **test database** (or transactions rolled back per test) for isolation.

**Key point:** use `supertest` against an exported `app` (no `listen`) to test routes/middleware in-process; separate unit tests (mocked deps) from integration tests (real DB), and isolate state per test.
