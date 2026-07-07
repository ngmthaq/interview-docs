# 5. How do you parse request bodies in Express? (Fresher)

Express doesn't parse request bodies by default — you add **built-in middleware** to populate `req.body`.

```ts
import express from "express";
const app = express();

app.use(express.json()); // parse JSON bodies (application/json)
app.use(express.urlencoded({ extended: true })); // parse form bodies

app.post("/users", (req, res) => {
  const { name, email } = req.body; // now available
  res.status(201).json({ name, email });
});
```

**Key parsers:**

- **`express.json()`** — parses `application/json` into `req.body`.
- **`express.urlencoded()`** — parses HTML form submissions (`application/x-www-form-urlencoded`).
- **`multer`** (third-party) — handles `multipart/form-data` file uploads.

**Notes:**

- Set a **size limit** to prevent abuse: `express.json({ limit: "100kb" })`.
- Without these, `req.body` is `undefined`.
- Register parsers **before** the routes that need them.

**Key point:** add `express.json()` / `express.urlencoded()` middleware to populate `req.body`; use `multer` for file uploads, always cap body size, and register parsers before your routes.
