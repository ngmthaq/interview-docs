# 13. What are Server Actions? (Mid)

**Server Actions** are async functions that run **on the server** but can be called directly from components (including forms) — letting you mutate data without manually building an API endpoint. Marked with the **`"use server"`** directive.

```tsx
// app/todos/actions.ts
"use server";
import { revalidatePath } from "next/cache";

export async function createTodo(formData: FormData) {
  const title = formData.get("title") as string;
  await db.todo.create({ data: { title } });
  revalidatePath("/todos"); // refresh the cached page
}
```

Use it directly in a form — no fetch, no route handler:

```tsx
import { createTodo } from "./actions";

export default function TodoForm() {
  return (
    <form action={createTodo}>
      <input name="title" />
      <button type="submit">Add</button>
    </form>
  );
}
```

**Notes:**

- Progressive enhancement — forms work even before JS loads.
- Pair with `revalidatePath`/`revalidateTag` to update cached data, and `useFormStatus`/`useActionState` for pending/optimistic UI.
- Always **validate & authorize** inside the action — it's a public server entry point.

**Key point:** Server Actions (`"use server"`) are server-run functions callable from forms/components for mutations without a separate API route; combine them with `revalidatePath`/`revalidateTag` to refresh data, and always validate/authorize since they're public endpoints.
