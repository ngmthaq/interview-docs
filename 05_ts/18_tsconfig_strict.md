# 18. `tsconfig` strict mode and key compiler options? (Mid)

`"strict": true` enables a bundle of safety flags. The important ones:

| Flag                           | Effect                                            |
| ------------------------------ | ------------------------------------------------- |
| `strictNullChecks`             | `null`/`undefined` not assignable unless declared |
| `noImplicitAny`                | error on inferred `any`                           |
| `strictFunctionTypes`          | stricter (contravariant) function param checks    |
| `strictPropertyInitialization` | class fields must be initialized                  |
| `noImplicitThis`               | error on untyped `this`                           |

```ts
// with strictNullChecks:
let name: string = null; // ❌
let name2: string | null = null; // ✅
```

**Other commonly tuned options:**

- `target` / `module` — JS version and module system to emit.
- `lib` — which built-in type libs (`DOM`, `ES2022`…).
- `noUnusedLocals` / `noUnusedParameters` — flag dead variables.
- `noImplicitReturns` — every code path must return.
- `esModuleInterop` — smooth CommonJS/ESM default imports.
- `paths` / `baseUrl` — path aliases (`@/utils`).
- `skipLibCheck` — skip type-checking `.d.ts` files (faster builds).

**Best practice:** always start new projects with `"strict": true` — retrofitting it later is painful.
