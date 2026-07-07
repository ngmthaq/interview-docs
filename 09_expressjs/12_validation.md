# 12. How do you validate request data? (Mid)

Never trust client input — **validate and sanitize** before it reaches business logic. Do it in middleware so handlers receive clean data.

**With Zod** (schema-first, TypeScript-friendly):

```ts
import { z } from "zod";

const createUserSchema = z.object({
  name: z.string().min(1),
  email: z.string().email(),
  age: z.number().int().positive().optional(),
});

const validate = (schema) => (req, res, next) => {
  const result = schema.safeParse(req.body);
  if (!result.success) {
    return res.status(400).json({ errors: result.error.flatten() });
  }
  req.body = result.data; // parsed & typed
  next();
};

app.post("/users", validate(createUserSchema), createUser);
```

**Options:** `zod`, `joi`, `express-validator`, `class-validator` (NestJS-style).

**Best practices:**

- Validate **body, params, and query**.
- Return **400** with a clear, structured error list.
- **Coerce/transform** types (strings → numbers) and strip unknown fields.

**Key point:** validate all input in middleware with a schema library (Zod/Joi) before it hits handlers, returning 400 with structured errors — this centralizes safety and gives handlers clean, typed data.
