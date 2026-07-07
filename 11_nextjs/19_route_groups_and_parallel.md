# 19. What are route groups, parallel, and intercepting routes? (Mid)

Advanced App Router conventions using special folder syntax for organization and complex layouts.

**Route Groups `(folder)`** — organize routes **without** affecting the URL:

```
app/
├── (marketing)/about/page.tsx   →  /about   (group name ignored in URL)
├── (marketing)/layout.tsx       →  shared layout for marketing pages
└── (shop)/cart/page.tsx         →  /cart
```

Useful for applying **different layouts** to different sections.

**Parallel Routes `@folder`** — render multiple pages in the **same layout** simultaneously (slots):

```tsx
// app/layout.tsx receives named slots
export default function Layout({ children, team, analytics }) {
  return (
    <>
      {children}
      {team}
      {analytics}
    </>
  );
}
// app/@team/page.tsx and app/@analytics/page.tsx fill the slots
```

Great for dashboards showing independent sections.

**Intercepting Routes `(.)folder`** — load a route **within the current layout** (e.g. show a photo in a modal over the feed, but a full page on direct visit).

**Key point:** route groups `(name)` organize files and layouts without changing URLs; parallel routes `@slot` render multiple independent pages in one layout; intercepting routes `(.)` load a route in-context (like modals) — advanced conventions for sophisticated layouts.
