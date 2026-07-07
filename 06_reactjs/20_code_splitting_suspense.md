# 20. Code splitting with `lazy` and `Suspense`? (Senior)

**Code splitting** breaks the bundle into chunks loaded **on demand**, so users don't download the whole app upfront — improving initial load time.

**`React.lazy`** dynamically imports a component; **`Suspense`** shows a fallback while it loads:

```tsx
const Dashboard = React.lazy(() => import("./Dashboard"));

function App() {
  return (
    <Suspense fallback={<Spinner />}>
      <Dashboard /> {/* loaded only when rendered */}
    </Suspense>
  );
}
```

The `import()` produces a **separate chunk** that the bundler (Webpack/Vite) serves lazily.

**Common split points:**

- **Routes** — each page as its own chunk (biggest win).
- **Heavy components** — charts, editors, modals shown conditionally.
- **Below-the-fold** content.

**`Suspense`** is broader than lazy loading — it lets a component "wait" for something (code, and with frameworks, **data**) and declaratively render a fallback. React 18 added Suspense for data fetching and streaming SSR.

**Pair with an error boundary** to handle chunk load failures:

```tsx
<ErrorBoundary fallback={<RetryUI />}>
  <Suspense fallback={<Spinner />}>
    <Dashboard />
  </Suspense>
</ErrorBoundary>
```

**Concurrent companions:** `useTransition` / `useDeferredValue` keep the UI responsive while heavy content loads without blocking input.
