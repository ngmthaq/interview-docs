# 19. Error boundaries? (Senior)

An error boundary is a component that **catches JavaScript errors in its child tree during render**, logs them, and shows a fallback UI instead of crashing the whole app (React unmounts the tree on an uncaught render error).

**Only class components can be error boundaries** — via `getDerivedStateFromError` and/or `componentDidCatch`:

```tsx
class ErrorBoundary extends React.Component<
  { fallback: React.ReactNode; children: React.ReactNode },
  { hasError: boolean }
> {
  state = { hasError: false };

  static getDerivedStateFromError() {
    return { hasError: true }; // render fallback
  }
  componentDidCatch(error: Error, info: React.ErrorInfo) {
    logToService(error, info); // side effect: report
  }
  render() {
    return this.state.hasError ? this.props.fallback : this.props.children;
  }
}
```

```tsx
<ErrorBoundary fallback={<p>Something went wrong</p>}>
  <Dashboard />
</ErrorBoundary>
```

**What they DON'T catch:**

- Errors in **event handlers** (use `try/catch`).
- **Asynchronous** code (`setTimeout`, promises).
- **Server-side rendering** errors.
- Errors in the **boundary itself**.

**Best practice:** place boundaries strategically (around routes, widgets) so one failing section doesn't take down the page. Libraries like `react-error-boundary` provide a hook-friendly wrapper, but the boundary itself is still class-based.
