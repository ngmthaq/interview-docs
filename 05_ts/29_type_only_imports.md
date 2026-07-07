# 29. What are type-only imports and exports? (Mid)

**`import type`** / **`export type`** import or export **only type information**, which is **erased** at compile time — no runtime import is emitted.

```ts
import type { User } from "./models"; // erased from JS output
import { fetchUser } from "./api"; // real runtime import

// Mixed, with inline type markers:
import { type Config, loadConfig } from "./config";
```

**Why it matters:**

- **Avoids side effects / circular dependencies** — a type-only import never triggers module execution.
- **Smaller, clearer output** — bundlers know the import can be dropped entirely.
- **`verbatimModuleSyntax`** / `isolatedModules` may **require** `import type` so single-file transpilers (Babel, esbuild, SWC) know what to erase without type info.

**Type-only exports:**

```ts
export type { User, Role }; // re-export types without runtime code
```

**Key point:** `import type`/`export type` (and inline `type` markers) import/export types that are erased at build time — preventing accidental runtime imports and circular-dependency side effects, and satisfying `verbatimModuleSyntax`/`isolatedModules` so per-file transpilers can strip types correctly.
