# 14. What are custom providers? (Mid)

Beyond the standard `providers: [MyService]` shorthand, Nest supports **custom providers** for advanced DI — useful for interfaces, config values, or dynamic construction.

**Four forms:**

```ts
// 1. useClass — swap the implementation behind a token
{ provide: PaymentService, useClass: StripePaymentService }

// 2. useValue — inject a constant/mock
{ provide: "CONFIG", useValue: { apiUrl: "https://api.example.com" } }

// 3. useFactory — build dynamically, with injected deps
{
  provide: "DB_CONNECTION",
  useFactory: async (config: ConfigService) => createConnection(config.get("DB_URL")),
  inject: [ConfigService],
}

// 4. useExisting — alias to another provider
{ provide: "AliasToken", useExisting: RealService }
```

Inject non-class tokens with `@Inject`:

```ts
constructor(@Inject("CONFIG") private config: AppConfig) {}
```

**Why:** decouple from concrete classes (program to interfaces), inject config/constants, or perform async setup (DB connections).

**Key point:** custom providers (`useClass`/`useValue`/`useFactory`/`useExisting`) give fine-grained control over DI — bind interfaces to implementations, inject constants, or build dependencies asynchronously via factories, injected by custom tokens with `@Inject`.
