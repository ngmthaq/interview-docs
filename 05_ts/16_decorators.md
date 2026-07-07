# 16. Decorators? (Senior)

A decorator is a **function that annotates/modifies** a class, method, accessor, property, or parameter. Widely used by NestJS, Angular, and TypeORM.

```ts
function Log(target: any, key: string, desc: PropertyDescriptor) {
  const original = desc.value;
  desc.value = function (...args: any[]) {
    console.log(`calling ${key}`, args);
    return original.apply(this, args);
  };
}

class Service {
  @Log
  save(id: number) {
    /* ... */
  }
}
```

**Types of decorators:** class, method, accessor, property, parameter.

**Decorator factory** — a function returning a decorator, so you can pass config:

```ts
function Route(path: string) {
  return function (target: any, key: string) {
    Reflect.defineMetadata("path", path, target, key);
  };
}
class Ctrl {
  @Route("/users") list() {}
}
```

**Note on versions:** there are two flavors —

- **Legacy** (experimental): needs `"experimentalDecorators": true`; used by Angular/Nest/TypeORM.
- **Stage 3 / ECMAScript** decorators: standardized, different signature, default in TS 5+ without the flag.

Metadata reflection (`reflect-metadata`) requires `"emitDecoratorMetadata": true`.
