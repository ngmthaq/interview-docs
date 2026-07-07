# 20. What are dynamic modules? (Mid)

A **dynamic module** is a module configured at import time via a static method (commonly **`forRoot`** / **`forFeature`**), returning module metadata. This is how configurable modules (`ConfigModule`, `TypeOrmModule`) accept options.

```ts
@Module({})
export class DatabaseModule {
  static forRoot(options: DbOptions): DynamicModule {
    return {
      module: DatabaseModule,
      providers: [{ provide: "DB_OPTIONS", useValue: options }, DatabaseService],
      exports: [DatabaseService],
      global: true, // optional — make it globally available
    };
  }
}

// consumed with configuration
@Module({
  imports: [DatabaseModule.forRoot({ url: process.env.DB_URL })],
})
export class AppModule {}
```

**Conventions:**

- **`forRoot`** — configure once at the root (global setup, connections).
- **`forFeature`** — register feature-specific pieces (e.g. entity repositories).
- **`forRootAsync`** — async config, injecting `ConfigService` via `useFactory`.

**Key point:** dynamic modules return their metadata from a static method (`forRoot`/`forFeature`/`forRootAsync`), letting a module be configured with options at import time — the pattern behind every configurable Nest module.
