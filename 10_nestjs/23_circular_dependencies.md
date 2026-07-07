# 23. How do you handle circular dependencies? (Senior)

A **circular dependency** occurs when two providers (or modules) depend on each other — `A` needs `B` and `B` needs `A`. Nest can't resolve the injection order, throwing at startup.

**Fix with `forwardRef`:**

```ts
// Provider ↔ provider
@Injectable()
export class UsersService {
  constructor(
    @Inject(forwardRef(() => AuthService))
    private authService: AuthService,
  ) {}
}

// Module ↔ module
@Module({
  imports: [forwardRef(() => AuthModule)],
})
export class UsersModule {}
```

**Better: avoid the cycle.** Circular deps are often a **design smell**. Options:

- Extract the shared logic into a **third module/service** both depend on.
- Use an **event-based** approach (`EventEmitter`) to decouple.
- Re-examine responsibilities — the two classes may be too tightly coupled.

**Key point:** `forwardRef(() => X)` resolves unavoidable circular dependencies on both providers, but a cycle usually signals a design problem — prefer extracting shared logic into a third module or decoupling via events.
