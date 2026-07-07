# 8. Common utility types? (Mid)

Built-in generics that transform existing types — no need to hand-write variants.

```ts
interface User {
  id: number;
  name: string;
  email: string;
}
```

| Utility           | Result                           |
| ----------------- | -------------------------------- |
| `Partial<User>`   | all props optional               |
| `Required<User>`  | all props required               |
| `Readonly<User>`  | all props readonly               |
| `Pick<User,"id">` | `{ id: number }`                 |
| `Omit<User,"id">` | `{ name; email }`                |
| `Record<K,V>`     | object with keys `K`, values `V` |
| `ReturnType<F>`   | return type of a function type   |
| `Parameters<F>`   | tuple of a function's params     |
| `NonNullable<T>`  | removes `null` / `undefined`     |
| `Awaited<T>`      | unwraps a `Promise`              |

```ts
type Draft = Partial<User>; // { id?; name?; email? }
type Preview = Pick<User, "id" | "name">;
type Roles = Record<string, boolean>; // { [k: string]: boolean }

function getUser() {
  return { id: 1, name: "A" };
}
type U = ReturnType<typeof getUser>; // { id: number; name: string }
type P = Awaited<Promise<number>>; // number
```

**Why:** derive types from a single source of truth so they stay in sync.
