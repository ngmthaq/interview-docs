# 6. How does dependency injection work in NestJS? (Junior)

Nest has a built-in **IoC (Inversion of Control) container** that instantiates classes and **injects** their dependencies automatically, based on constructor parameter types.

```ts
@Injectable()
export class OrdersService {
  // Nest sees the types and injects instances
  constructor(
    private readonly paymentService: PaymentService,
    private readonly usersService: UsersService,
  ) {}
}
```

**How it resolves:**

1. A class requests a dependency via its constructor.
2. Nest looks up a **provider** matching that type (its **injection token**).
3. It creates (or reuses) the instance and passes it in.

**Why DI matters:**

- **Decoupling** — classes depend on abstractions, not concrete construction.
- **Testability** — swap real providers for mocks in tests.
- **Reuse** — a single shared instance (singleton) across the app.

The default **token** is the class itself; for interfaces or values, use a **custom token** with `@Inject("TOKEN")`.

**Key point:** Nest's IoC container auto-injects dependencies by reading constructor parameter types and matching them to registered providers — this decouples classes, enables easy mocking in tests, and defaults to singleton instances.
