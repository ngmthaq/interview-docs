# 3. How does file-based routing work in Nuxt? (Fresher)

Nuxt generates routes automatically from the **`pages/`** directory — each `.vue` file becomes a route. No manual Vue Router configuration.

```
pages/
├── index.vue          →  /
├── about.vue          →  /about
├── blog/
│   ├── index.vue      →  /blog
│   └── [slug].vue     →  /blog/:slug   (dynamic)
└── users/
    └── [id]/
        └── profile.vue →  /users/:id/profile
```

**Key facts:**

- **`index.vue`** maps to the folder's root path.
- **`[param].vue`** — dynamic segment, accessed via `useRoute().params`.
- **`[...slug].vue`** — catch-all route.
- Nested folders create nested URL paths.

```vue
<!-- pages/blog/[slug].vue -->
<script setup>
const route = useRoute();
const { data: post } = await useFetch(`/api/posts/${route.params.slug}`);
</script>
```

**Note:** the `pages/` directory is optional — if absent, Nuxt runs as a single-page app using `app.vue` only.

**Key point:** files in `pages/` become routes automatically — `index.vue` for the root, `[param].vue` for dynamic segments, `[...slug].vue` for catch-all — with params read via `useRoute()`, no manual router setup needed.
