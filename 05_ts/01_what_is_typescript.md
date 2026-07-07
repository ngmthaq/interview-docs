# 1. What is TypeScript and why use it? (Fresher)

TypeScript is a **superset of JavaScript** that adds **static types**. It compiles ("transpiles") down to plain JavaScript — the types are erased and add **zero runtime cost**.

```ts
function greet(name: string): string {
  return `Hi ${name}`;
}

greet(42); // ❌ compile-time error, caught before running
```

**Why teams use it:**

- **Catch bugs early** — type errors surface at compile time, not in production.
- **Better tooling** — autocomplete, refactoring, and inline docs in the editor.
- **Self-documenting** — signatures describe intent without extra comments.
- **Safer refactors** — rename a field and the compiler flags every broken usage.

**Key point:** types exist only at **compile time**. At runtime it is just JavaScript — you cannot check a TypeScript type with `if (x is SomeType)`.
