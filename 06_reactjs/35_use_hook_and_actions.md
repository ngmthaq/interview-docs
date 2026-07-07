# 35. The `use` hook and Actions (React 19). (Senior)

React 19 introduced the **`use`** API and **Actions** to simplify reading async resources and handling form mutations.

**`use(promise)`** — read a promise (or context) during render; suspends until it resolves:

```tsx
import { use, Suspense } from "react";

function Comments({ commentsPromise }) {
  const comments = use(commentsPromise); // suspends until resolved
  return comments.map((c) => <p key={c.id}>{c.text}</p>);
}

// Parent provides the promise + a Suspense boundary
<Suspense fallback={<Spinner />}>
  <Comments commentsPromise={fetchComments()} />
</Suspense>;
```

Unlike hooks, **`use` can be called conditionally** (inside `if`/loops) and also reads context.

**Actions** — async functions wired to forms/transitions with built-in pending/error handling:

```tsx
function AddToCart() {
  const [state, formAction, isPending] = useActionState(
    async (prev, formData) => {
      await addItem(formData.get("id"));
      return { success: true };
    },
    { success: false },
  );
  return <form action={formAction}>{isPending ? "Adding…" : <button>Add</button>}</form>;
}
```

Related hooks: **`useFormStatus`** (pending state of the enclosing form) and **`useOptimistic`** (optimistic UI).

**Key point:** React 19's `use(promise)` reads async resources during render with Suspense (and can be called conditionally), while Actions + `useActionState`/`useFormStatus`/`useOptimistic` standardize async form mutations with built-in pending, error, and optimistic states.
