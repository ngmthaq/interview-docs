# 26. How do you implement caching in NestJS? (Senior)

Nest's **`CacheModule`** provides a unified cache abstraction with pluggable stores (in-memory by default, or Redis for distributed caching).

```ts
@Module({
  imports: [
    CacheModule.registerAsync({
      useFactory: (config: ConfigService) => ({
        store: redisStore,
        host: config.get("REDIS_HOST"),
        ttl: 60, // seconds
      }),
      inject: [ConfigService],
    }),
  ],
})
export class AppModule {}
```

**Auto-cache GET routes** with the interceptor:

```ts
@UseInterceptors(CacheInterceptor)
@Get()
findAll() {
  return this.service.findAll(); // response cached by URL
}
```

**Manual control** — inject the cache manager:

```ts
@Injectable()
export class UsersService {
  constructor(@Inject(CACHE_MANAGER) private cache: Cache) {}

  async findOne(id: string) {
    const cached = await this.cache.get(`user:${id}`);
    if (cached) return cached;
    const user = await this.repo.findOne(id);
    await this.cache.set(`user:${id}`, user, { ttl: 300 });
    return user;
  }
}
```

**Key point:** `CacheModule` abstracts caching with swappable stores (in-memory → Redis for clustering); use `CacheInterceptor` to auto-cache GET responses or inject `CACHE_MANAGER` for manual get/set with per-key TTLs — and mind invalidation on writes.
