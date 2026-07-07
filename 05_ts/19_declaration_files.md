# 19. Declaration files (`.d.ts`) and modules? (Mid)

A **`.d.ts`** file contains **type declarations only** — no implementation. It describes the shape of JavaScript code so TypeScript can type-check against it.

```ts
// math.d.ts
export function add(a: number, b: number): number;
export const PI: number;
```

**Where they come from:**

- `tsc --declaration` generates them from your `.ts` source (for publishing libraries).
- **`@types/*`** packages (DefinitelyTyped) provide types for untyped JS libs: `npm i -D @types/node`.
- Hand-written to describe globals or untyped modules.

**Declaring an untyped module** so imports stop erroring:

```ts
// globals.d.ts
declare module "untyped-lib" {
  export function doThing(): void;
}
declare module "*.svg" {
  const url: string;
  export default url;
}
```

**Ambient globals:**

```ts
declare const __VERSION__: string; // injected by bundler
```

**`declare`** means "this exists at runtime, defined elsewhere — just trust the type."

**Related — modules vs namespaces:** modern code uses ES **modules** (`import`/`export`). **Namespaces** (`namespace X {}`) are an older internal-module system, now mainly seen in global `.d.ts` files.
