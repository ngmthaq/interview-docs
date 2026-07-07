# 3. `any` vs `unknown` vs `never`? (Mid)

|           | Meaning                          | Assignable to it | Assignable from it     |
| --------- | -------------------------------- | ---------------- | ---------------------- |
| `any`     | Turn off type checking           | anything         | anything               |
| `unknown` | Top type — "something, unknown"  | anything         | nothing until narrowed |
| `never`   | Bottom type — value never occurs | nothing          | anything               |

```ts
let a: any = 5;
a.foo.bar(); // ✅ compiles — no safety, defeats TypeScript

let u: unknown = 5;
u.toFixed(); // ❌ must narrow first
if (typeof u === "number") u.toFixed(); // ✅

function fail(msg: string): never {
  throw new Error(msg); // never returns
}
```

- **`any`** — escape hatch; avoid it, it silently disables checks.
- **`unknown`** — the _safe_ `any`: forces you to narrow before use.
- **`never`** — functions that never return, and exhaustiveness checks in a `switch`.

**Tip:** prefer `unknown` over `any` for untyped input (e.g. `JSON.parse`, API responses).
