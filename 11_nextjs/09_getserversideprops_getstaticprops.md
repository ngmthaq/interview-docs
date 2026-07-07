# 9. getStaticProps vs getServerSideProps (Pages Router). (Junior)

In the **Pages Router**, these special exported functions fetch data server-side and pass it as props.

**`getStaticProps`** — runs at **build time** (SSG):

```tsx
export async function getStaticProps() {
  const posts = await getPosts();
  return {
    props: { posts },
    revalidate: 60, // opt into ISR — regenerate at most every 60s
  };
}
```

**`getServerSideProps`** — runs on **every request** (SSR):

```tsx
export async function getServerSideProps(context) {
  const { req, params, query } = context;
  const data = await getData(params.id);
  return { props: { data } };
}
```

**`getStaticPaths`** — pre-generate dynamic routes for SSG:

```tsx
export async function getStaticPaths() {
  return { paths: [{ params: { id: "1" } }], fallback: "blocking" };
}
```

|                | `getStaticProps` | `getServerSideProps` |
| -------------- | ---------------- | -------------------- |
| When           | Build time       | Each request         |
| Strategy       | SSG (+ISR)       | SSR                  |
| Data freshness | Static/periodic  | Always fresh         |

**Note:** these are **Pages Router only**; the App Router replaces them with async components + `fetch`.

**Key point:** `getStaticProps` (build-time, SSG, optional `revalidate` for ISR) and `getServerSideProps` (per-request, SSR) are the Pages Router's data-fetching functions — superseded by async Server Components in the App Router.
