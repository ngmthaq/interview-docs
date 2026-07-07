# 20. How do you handle server-only vs client-only code? (Mid)

In SSR, component code runs on **both** the server and the client. Some code (browser APIs, certain libraries) must run on **one side only**.

**Detecting the environment:**

```ts
if (import.meta.server) {
  // runs only during server render
}
if (import.meta.client) {
  // runs only in the browser (window, localStorage available)
}
```

**Client-only rendering — `<ClientOnly>`:**

```vue
<template>
  <ClientOnly>
    <BrowserOnlyChart />
    <!-- skipped during SSR -->
    <template #fallback><Spinner /></template>
  </ClientOnly>
</template>
```

**Other tools:**

- **`.client.vue`** / **`.server.vue`** component suffixes — render only on that side.
- **`.client.ts`** / **`.server.ts`** plugins — run on one side.
- Use **`onMounted`** for browser-only logic (it never runs on the server).

**Why it matters:** accessing `window`/`document` during SSR throws; mismatched server/client output causes **hydration errors**.

**Key point:** guard side-specific code with `import.meta.server`/`import.meta.client`, wrap browser-only UI in `<ClientOnly>`, use `.client`/`.server` suffixes, and put browser logic in `onMounted` — avoiding SSR crashes and hydration mismatches.
