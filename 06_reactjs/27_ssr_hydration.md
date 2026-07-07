# 27. CSR vs SSR vs hydration? (Senior)

**How the HTML gets built and made interactive:**

| Strategy | HTML generated            | Pros                  | Cons                                |
| -------- | ------------------------- | --------------------- | ----------------------------------- |
| **CSR**  | in the browser            | simple, cheap server  | blank page until JS loads; weak SEO |
| **SSR**  | on the server per request | fast first paint, SEO | server cost, TTFB                   |
| **SSG**  | at build time             | fastest, cacheable    | stale until rebuild                 |
| **ISR**  | build + revalidate        | SSG + freshness       | framework-specific                  |

**CSR** — server sends an empty `<div id="root">` + JS bundle; React renders everything client-side.

**SSR** — server runs React to a string (`renderToString` / `renderToPipeableStream`), sends **ready HTML** so the user sees content immediately.

**Hydration** — the client then **attaches event listeners and state** to that server-rendered HTML, making it interactive without re-creating the DOM:

```tsx
import { hydrateRoot } from "react-dom/client";
hydrateRoot(document.getElementById("root")!, <App />);
```

**Hydration mismatch** — if server and client render different markup, React warns and may discard the server HTML. Causes: `Date.now()`, `Math.random()`, `window`/`localStorage` during render, locale-dependent formatting. Fix by rendering such values in `useEffect` after mount.

**Modern React (18/19):** **streaming SSR** + **Suspense** send HTML in chunks, and **selective hydration** hydrates interactive parts first. **React Server Components** push this further — some components run only on the server and ship zero JS.
