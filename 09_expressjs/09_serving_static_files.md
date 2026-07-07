# 9. How do you serve static files? (Junior)

The built-in **`express.static`** middleware serves files (HTML, CSS, images, JS bundles) directly from a directory.

```ts
import express from "express";
import path from "path";

const app = express();

// Serve everything in ./public at the root URL
app.use(express.static(path.join(__dirname, "public")));
// public/logo.png  →  GET /logo.png

// Serve under a virtual path prefix
app.use("/static", express.static("public"));
// public/logo.png  →  GET /static/logo.png
```

**Useful options:**

```ts
app.use(
  express.static("public", {
    maxAge: "1d", // cache-control header
    etag: true, // enable ETag validation
    index: "index.html", // default file for a directory
  }),
);
```

**Notes:**

- For production, a **CDN or reverse proxy** (nginx) often serves static assets more efficiently than Node.
- Place `express.static` early so asset requests short-circuit before hitting API routes.

**Key point:** `express.static(dir)` serves files from a folder, optionally under a URL prefix and with caching options — great for dev and small apps, though a CDN/reverse proxy is preferred for static assets at scale.
