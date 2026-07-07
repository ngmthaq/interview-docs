# 2. `type` vs `interface`? (Fresher)

Both describe the shape of an object. They overlap ~90%; the differences are at the edges.

|                    | `interface`      | `type`                |
| ------------------ | ---------------- | --------------------- |
| Object shapes      | ✅               | ✅                    |
| Unions / tuples    | ❌               | ✅ `type T = A \| B`  |
| Primitives/aliases | ❌               | ✅ `type ID = string` |
| Extends            | `extends`        | `&` (intersection)    |
| Declaration merge  | ✅ re-open & add | ❌ duplicate = error  |

```ts
interface User {
  id: number;
}
interface User {
  name: string;
} // merged: { id, name }

type Status = "on" | "off"; // only type can do unions
type Point = [number, number]; // and tuples
```

**Rule of thumb:** use `interface` for public object/class shapes (mergeable, familiar `extends`); use `type` for unions, tuples, primitives, and complex composed types.
