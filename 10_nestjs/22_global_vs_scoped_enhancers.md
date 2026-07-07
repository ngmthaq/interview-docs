# 22. Global vs scoped enhancers (guards/pipes/interceptors/filters). (Senior)

Guards, pipes, interceptors, and filters can be applied at **method**, **controller**, or **global** scope — with an important DI caveat for globals.

**Applying globally two ways:**

```ts
// 1. Instance-based — simple, but NO dependency injection
app.useGlobalGuards(new AuthGuard());

// 2. DI-based — register as a provider so it CAN inject dependencies
@Module({
  providers: [
    { provide: APP_GUARD, useClass: AuthGuard },
    { provide: APP_PIPE, useClass: ValidationPipe },
    { provide: APP_INTERCEPTOR, useClass: LoggingInterceptor },
    { provide: APP_FILTER, useClass: AllExceptionsFilter },
  ],
})
export class AppModule {}
```

**Why the second form matters:**

- `app.useGlobalGuards(new X())` is instantiated **outside** the DI container, so it **can't inject** services.
- Using the `APP_*` tokens registers the enhancer as a provider — Nest injects its dependencies normally.

**Scope precedence:** global runs outermost, then controller, then method.

**Key point:** for global guards/pipes/interceptors/filters that need injected dependencies, register them with the `APP_GUARD`/`APP_PIPE`/`APP_INTERCEPTOR`/`APP_FILTER` provider tokens rather than `app.useGlobalX(new X())`, which bypasses DI.
