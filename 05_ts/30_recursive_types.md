# 30. What are recursive types? (Senior)

A **recursive type** references itself — essential for modeling nested/tree-like structures (JSON, file trees, linked lists, nested comments).

```ts
// A JSON value
type Json = string | number | boolean | null | Json[] | { [key: string]: Json };

const data: Json = { name: "Ada", tags: ["a", "b"], meta: { active: true } };
```

**Tree structures:**

```ts
interface TreeNode<T> {
  value: T;
  children: TreeNode<T>[]; // self-reference
}
```

**Recursive utility types** (type-level recursion):

```ts
// Deeply readonly
type DeepReadonly<T> = {
  readonly [K in keyof T]: T[K] extends object ? DeepReadonly<T[K]> : T[K];
};

// Deep partial
type DeepPartial<T> = {
  [K in keyof T]?: T[K] extends object ? DeepPartial<T[K]> : T[K];
};
```

**Notes:**

- TypeScript allows recursion in type aliases and conditional/mapped types.
- There's a **recursion depth limit** (~50 levels) to prevent infinite loops; extremely deep types may error.

**Key point:** recursive types reference themselves to model nested data (JSON, trees) and enable deep type transformations (`DeepReadonly`, `DeepPartial`) via recursive mapped/conditional types — powerful, though bounded by TypeScript's recursion depth limit.
