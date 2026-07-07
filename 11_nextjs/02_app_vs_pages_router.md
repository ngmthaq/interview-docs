# 2. App Router vs Pages Router. (Fresher)

Next.js has two routing systems. The **Pages Router** (`pages/`) is the original; the **App Router** (`app/`) is the modern default since Next 13, built around **React Server Components**.

| Feature       | Pages Router (`pages/`)                 | App Router (`app/`)          |
| ------------- | --------------------------------------- | ---------------------------- |
| Routing file  | `pages/about.tsx`                       | `app/about/page.tsx`         |
| Components    | Client by default                       | **Server** by default        |
| Data fetching | `getServerSideProps` / `getStaticProps` | `async` components + `fetch` |
| Layouts       | `_app.tsx` (manual)                     | Nested `layout.tsx`          |
| Streaming     | No                                      | Yes (Suspense)               |

```tsx
// App Router — app/about/page.tsx
export default async function About() {
  const data = await getData(); // fetch directly in the component
  return <main>{data.title}</main>;
}
```

**Notes:**

- The **App Router** is recommended for new projects (server components, layouts, streaming).
- Both can **coexist** in one app during migration.

**Key point:** the App Router (`app/`) is the modern default — server components, nested layouts, streaming, and in-component data fetching — while the Pages Router (`pages/`) is the legacy system with `getServerSideProps`/`getStaticProps`; new apps should use App Router.
