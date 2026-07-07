# 16. What are plugins in Nuxt? (Mid)

**Plugins** (files in **`plugins/`**) run **once when the app is created** — the place to register Vue plugins, inject helpers, or set up libraries. They're auto-registered.

```ts
// plugins/hello.ts
export default defineNuxtPlugin((nuxtApp) => {
  // Provide a helper available everywhere as $hello / useNuxtApp().$hello
  return {
    provide: {
      hello: (name: string) => `Hello, ${name}!`,
    },
  };
});
```

Use the injected helper:

```vue
<script setup>
const { $hello } = useNuxtApp();
console.log($hello("Ada"));
</script>
```

**Controlling execution:**

- **`.client.ts`** / **`.server.ts`** suffix — run only on that side (e.g. a browser-only library `.client.ts`).
- Register a **Vue plugin**: `nuxtApp.vueApp.use(SomePlugin)`.
- Order with a numeric prefix or `dependsOn` for ordering.

**Key point:** plugins in `plugins/` run at app creation via `defineNuxtPlugin` to register Vue plugins or inject helpers (`provide`); use `.client`/`.server` suffixes to scope them to one side — auto-registered, the standard extension point for third-party setup.
