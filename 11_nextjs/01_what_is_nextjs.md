# 1. What is Next.js? (Fresher)

**Next.js** is a **React framework** for building full-stack web applications. It adds structure and production features on top of React: **routing**, multiple **rendering strategies** (SSR, SSG, ISR), **server components**, an **API layer**, bundling, and optimizations — so you don't wire these up yourself.

```tsx
// app/page.tsx — a route rendered on the server by default
export default function HomePage() {
  return <h1>Welcome to Next.js</h1>;
}
```

**What Next.js gives you over plain React:**

- **File-based routing** — folders/files become routes (no React Router setup).
- **Rendering flexibility** — server-render, static-generate, or stream per route.
- **Full-stack** — build backend endpoints (Route Handlers / Server Actions) in the same project.
- **Built-in optimization** — image, font, and script optimization; automatic code splitting.

Maintained by **Vercel**, it's the most popular production React framework.

**Key point:** Next.js is a full-stack React framework providing file-based routing, flexible rendering (SSR/SSG/ISR), server components, and built-in optimizations — turning React from a UI library into a complete application framework.
