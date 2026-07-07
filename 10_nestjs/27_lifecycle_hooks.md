# 27. What are lifecycle hooks in NestJS? (Senior)

Nest exposes **lifecycle hooks** — interfaces you implement to run code at key moments of a provider/module or the whole app's life. Essential for setup and **graceful shutdown**.

```ts
@Injectable()
export class DatabaseService implements OnModuleInit, OnApplicationShutdown {
  async onModuleInit() {
    await this.connect(); // run once, after the module's deps are ready
  }

  async onApplicationShutdown(signal: string) {
    await this.disconnect(); // clean up on SIGTERM/SIGINT
  }
}
```

**Order of hooks:**

1. `onModuleInit` — module's dependencies resolved.
2. `onApplicationBootstrap` — all modules initialized.
3. _(app runs)_
4. `onModuleDestroy` — shutdown begins.
5. `beforeApplicationShutdown`
6. `onApplicationShutdown(signal)`

**Enable shutdown hooks** (they're off by default):

```ts
app.enableShutdownHooks(); // listen for SIGTERM/SIGINT
```

**Key point:** lifecycle hooks (`onModuleInit`, `onApplicationBootstrap`, `onModuleDestroy`, `onApplicationShutdown`) run setup/teardown at defined phases; call `app.enableShutdownHooks()` so DB connections, queues, and timers close cleanly on shutdown signals.
