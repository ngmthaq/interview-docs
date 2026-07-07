# 17. What are Nuxt modules? (Mid)

**Modules** are packages that **extend Nuxt** at build time — adding features, integrating libraries, or altering config via Nuxt's hooks. The ecosystem is a major Nuxt strength.

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  modules: [
    "@pinia/nuxt", // state management
    "@nuxtjs/tailwindcss", // styling
    "@nuxt/image", // image optimization
    "@nuxtjs/i18n", // internationalization
    "@nuxt/content", // file-based CMS
  ],
});
```

**Plugins vs modules:**

- **Plugins** run at **runtime** (app creation) in every request/client.
- **Modules** run at **build/dev time** — they can register plugins, add components, inject config, extend the server, and hook into the build.

**Writing a module:**

```ts
export default defineNuxtModule({
  setup(options, nuxt) {
    addPlugin(resolve("./runtime/plugin"));
    // add components, server routes, hooks, etc.
  },
});
```

**Key point:** modules extend Nuxt at build time (via `defineNuxtModule` and hooks) to add features/integrations — registered in `nuxt.config`'s `modules` array; unlike runtime plugins, they can inject plugins, components, config, and server routes into the app.
