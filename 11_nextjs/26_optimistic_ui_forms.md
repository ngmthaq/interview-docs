# 26. How do you build forms with pending and optimistic UI? (Senior)

Next.js + React provide hooks to show **pending states** and **optimistic updates** around Server Actions.

**Pending state — `useFormStatus`:**

```tsx
"use client";
import { useFormStatus } from "react-dom";

function SubmitButton() {
  const { pending } = useFormStatus();
  return <button disabled={pending}>{pending ? "Saving…" : "Save"}</button>;
}
```

**Action state & validation errors — `useActionState`:**

```tsx
"use client";
import { useActionState } from "react";

const [state, formAction] = useActionState(createTodo, { error: null });
// <form action={formAction}> ... {state.error && <p>{state.error}</p>}
```

**Optimistic updates — `useOptimistic`:**

```tsx
const [optimisticTodos, addOptimistic] = useOptimistic(todos);
// show the new item instantly, before the server confirms
```

**Flow:** the form's `action` calls a Server Action; `useFormStatus` disables the button while it runs, `useOptimistic` shows the result immediately, and `useActionState` surfaces validation errors returned by the action.

**Key point:** wire forms to Server Actions and layer React hooks — `useFormStatus` for pending UI, `useActionState` for returned errors/state, and `useOptimistic` for instant optimistic updates — to build responsive forms with progressive enhancement.
