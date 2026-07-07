# 16. How do you handle metadata and SEO? (Mid)

The App Router has a built-in **Metadata API** — export a `metadata` object or a `generateMetadata` function from a `layout`/`page`, and Next injects the `<head>` tags.

**Static metadata:**

```tsx
// app/about/page.tsx
import type { Metadata } from "next";

export const metadata: Metadata = {
  title: "About Us",
  description: "Learn about our company",
  openGraph: { title: "About Us", images: ["/og.png"] },
};
```

**Dynamic metadata** — depends on data/params:

```tsx
export async function generateMetadata({ params }): Promise<Metadata> {
  const { slug } = await params;
  const post = await getPost(slug);
  return { title: post.title, description: post.excerpt };
}
```

**Why Next.js is good for SEO:**

- **Server rendering** delivers full HTML to crawlers (vs empty CSR shells).
- **Metadata API** manages titles, descriptions, Open Graph, canonical, robots.
- File conventions for `sitemap.ts`, `robots.ts`, and dynamic `opengraph-image`.

**Key point:** use the Metadata API — a static `metadata` export or async `generateMetadata` — to set titles/descriptions/OG tags per route; combined with server rendering, this gives crawlers complete HTML, making Next.js strong for SEO.
