# 10. What are layouts and templates? (Junior)

**Layouts** are shared UI that **wrap** child routes and **persist** across navigation (they don't re-render when moving between sibling pages).

```tsx
// app/dashboard/layout.tsx — wraps every /dashboard/* route
export default function DashboardLayout({ children }: { children: React.ReactNode }) {
  return (
    <div>
      <Sidebar /> {/* stays mounted across navigation */}
      <main>{children}</main>
    </div>
  );
}
```

**Key facts:**

- The **root layout** (`app/layout.tsx`) is required and must contain `<html>` and `<body>`.
- Layouts **nest** — each segment's layout wraps its children, composing down the tree.
- Layouts **preserve state** (scroll, form input, component state) across navigation.

**Templates** (`template.tsx`) are like layouts but create a **new instance** on each navigation — so state resets and effects re-run. Use them when you need per-navigation re-initialization (e.g. enter animations).

**Key point:** layouts (`layout.tsx`) wrap child routes and persist across navigation (preserving state), nesting down the tree from a required root layout; templates (`template.tsx`) behave similarly but remount on each navigation when you need fresh state/effects.
