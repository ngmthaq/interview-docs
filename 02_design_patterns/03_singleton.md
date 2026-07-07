# 3. Explain the Singleton pattern. (Junior)

**Singleton** ensures a class has **exactly one instance** and provides a **global access point** to it. Useful for shared resources: config, logger, DB connection pool.

```ts
class Config {
  private static instance: Config;
  private constructor(public settings: Record<string, string> = {}) {}

  static getInstance(): Config {
    if (!Config.instance) {
      Config.instance = new Config();
    }
    return Config.instance;
  }
}

Config.getInstance() === Config.getInstance(); // true — same object
```

**How it works:** private constructor blocks `new`; a static method lazily creates and caches the one instance.

**Watch out (Senior nuance):**

- Singletons are effectively **global state** → can hurt testability and hide dependencies.
- Often better to use **dependency injection** with a single registered instance instead of a hard Singleton.
