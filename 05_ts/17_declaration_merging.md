# 17. Declaration merging? (Senior)

TypeScript can **merge multiple declarations with the same name** into a single definition.

**Interface merging** — re-open and add members:

```ts
interface Window {
  myGlobal: string;
}
// elsewhere
interface Window {
  analytics: object;
}
// window now has both myGlobal and analytics
```

This is how you **augment third-party / global types** without editing their source:

```ts
// augment Express Request with a user field
declare global {
  namespace Express {
    interface Request {
      user?: { id: string };
    }
  }
}
```

**Namespace + function/class merging** — attach static-like members:

```ts
function greet() {}
namespace greet {
  export const version = "1.0";
}
greet.version; // "1.0"
```

**Module augmentation** — extend an existing module's typings:

```ts
declare module "express" {
  interface Request {
    requestId: string;
  }
}
```

**Note:** `type` aliases **cannot** merge — duplicate `type` names are an error. Only interfaces, namespaces, enums, and functions/classes merge.
