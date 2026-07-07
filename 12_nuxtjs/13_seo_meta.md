# 13. How do you handle SEO and meta tags? (Mid)

Nuxt manages the document `<head>` with **`useHead`** and **`useSeoMeta`** composables (plus config-level defaults).

**`useSeoMeta`** — type-safe, SEO-focused:

```vue
<script setup>
const { data: post } = await useFetch(`/api/posts/${slug}`);

useSeoMeta({
  title: post.value.title,
  description: post.value.excerpt,
  ogTitle: post.value.title,
  ogImage: post.value.image,
  twitterCard: "summary_large_image",
});
</script>
```

**`useHead`** — general head management (scripts, links, arbitrary meta):

```vue
<script setup>
useHead({
  title: "My Page",
  meta: [{ name: "robots", content: "index,follow" }],
  link: [{ rel: "canonical", href: "https://example.com/page" }],
});
</script>
```

**Why Nuxt is good for SEO:**

- **SSR** delivers fully-rendered HTML to crawlers.
- App-wide defaults set in `nuxt.config.ts` under `app.head`.

**Key point:** use `useSeoMeta` for type-safe SEO tags (title, description, Open Graph, Twitter) and `useHead` for general head control (links, scripts, meta); combined with SSR, crawlers receive complete HTML — set global defaults in `nuxt.config`.
