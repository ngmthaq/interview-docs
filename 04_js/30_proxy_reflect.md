# 30. What are Proxy and Reflect? (Senior)

A **`Proxy`** wraps an object and **intercepts** fundamental operations (get, set, has, delete…) via **traps**. **`Reflect`** provides methods mirroring those operations, used to perform the default behavior inside traps.

```js
const target = { name: "Ada", age: 36 };

const proxy = new Proxy(target, {
  get(obj, prop, receiver) {
    console.log(`Reading ${String(prop)}`);
    return Reflect.get(obj, prop, receiver); // default behavior
  },
  set(obj, prop, value, receiver) {
    if (prop === "age" && typeof value !== "number") {
      throw new TypeError("age must be a number");
    }
    return Reflect.set(obj, prop, value, receiver);
  },
});

proxy.name; // logs "Reading name" → "Ada"
proxy.age = 40; // validated
```

**Common traps:** `get`, `set`, `has` (`in`), `deleteProperty`, `apply` (function calls), `construct` (`new`).

**Use cases:** reactive systems (**Vue 3's reactivity** uses Proxy), validation, logging/observability, default values, access control, negative array indices.

**Why `Reflect`:** it gives the correct default operation (with proper `receiver` handling for inheritance), making traps clean and forwardable.

**Key point:** `Proxy` intercepts object operations through traps (get/set/has/etc.) to add validation, reactivity, or logging transparently; `Reflect` supplies the default operations to call inside traps — together they power meta-programming like Vue's reactivity.
