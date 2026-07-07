# 6. What is express.Router? (Junior)

**`express.Router()`** creates a **modular, mountable** group of routes — a "mini-app" you can organize in separate files and attach to a base path. Essential for keeping large apps maintainable.

```ts
// routes/users.ts
import { Router } from "express";
const router = Router();

router.get("/", listUsers); // GET  /users
router.get("/:id", getUser); // GET  /users/:id
router.post("/", createUser); // POST /users

export default router;

// app.ts
import usersRouter from "./routes/users";
app.use("/users", usersRouter); // mount at /users
```

**Benefits:**

- **Modularity** — split routes by resource/domain into separate files.
- **Shared middleware** — apply middleware to a whole router: `router.use(authGuard)`.
- **Prefixing** — mount under a base path (`/api/v1/users`) without repeating it.

**Key point:** `express.Router()` groups related routes into reusable modules mounted at a base path — it's how you scale beyond a single file, apply per-group middleware, and keep routing organized.
