# 11. Explain the Proxy pattern. (Mid)

**Proxy** provides a **stand-in** for another object to control access to it — adding logic like lazy loading, caching, access control, or logging, while keeping the same interface.

```ts
interface Api {
  fetch(id: number): string;
}

class RealApi implements Api {
  fetch(id: number) {
    return `data-${id}`;
  } // expensive call
}

class CachingProxy implements Api {
  private cache = new Map<number, string>();
  constructor(private real: Api) {}

  fetch(id: number) {
    if (!this.cache.has(id)) {
      this.cache.set(id, this.real.fetch(id));
    }
    return this.cache.get(id)!;
  }
}

const api: Api = new CachingProxy(new RealApi());
```

**Common proxy types:**

- **Virtual** — lazy-init expensive objects.
- **Caching** — memoize results.
- **Protection** — enforce access rules.
- **Remote** — represent an object in another process/server.

**Proxy vs Decorator:** both wrap, but Proxy _controls access_; Decorator _adds behavior_.
