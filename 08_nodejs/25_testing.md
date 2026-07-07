# 25. How do you test a Node.js application? (Mid)

Node has a **built-in test runner** (`node:test`, stable in Node 20+), plus popular frameworks like **Jest** and **Vitest**.

```ts
import { test, describe } from "node:test";
import assert from "node:assert/strict";
import { add } from "./math.js";

describe("add", () => {
  test("sums two numbers", () => {
    assert.equal(add(2, 3), 5);
  });
});
// Run:  node --test
```

**Test levels:**

- **Unit** — a single function/module in isolation; mock external deps.
- **Integration** — modules together (e.g. service + real database).
- **E2E / API** — hit real HTTP endpoints (`supertest`).

```ts
import request from "supertest";
const res = await request(app).get("/health");
assert.equal(res.status, 200);
```

**Practices:**

- **Mock/stub** I/O (DB, network) in unit tests for speed and determinism.
- Track **coverage** (`node --test --experimental-test-coverage` or c8/nyc).
- Keep tests **isolated** — no shared mutable state between them.

**Key point:** use the built-in `node:test` (or Jest/Vitest) for unit/integration tests, `supertest` for API tests, mock external I/O for deterministic units, and measure coverage — structure tests as a pyramid (many unit, fewer E2E).
