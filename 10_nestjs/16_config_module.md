# 16. How do you manage configuration in NestJS? (Mid)

The official **`@nestjs/config`** package loads environment variables and exposes them via an injectable **`ConfigService`**.

```ts
import { ConfigModule, ConfigService } from "@nestjs/config";

@Module({
  imports: [
    ConfigModule.forRoot({
      isGlobal: true, // available everywhere without re-importing
      envFilePath: [".env"],
      validationSchema: envSchema, // validate env at startup (Joi)
    }),
  ],
})
export class AppModule {}
```

Inject and use it:

```ts
@Injectable()
export class AppService {
  constructor(private config: ConfigService) {}

  getDbUrl(): string {
    return this.config.get<string>("DATABASE_URL");
  }
}
```

**Best practices:**

- Set **`isGlobal: true`** so you don't re-import the module everywhere.
- **Validate** env vars at boot (Joi/Zod schema) — fail fast on misconfiguration.
- Use **namespaced config** (`registerAs`) and typed access for larger apps.
- Never commit `.env`; provide `.env.example`.

**Key point:** use `@nestjs/config` with a global `ConfigModule` and inject `ConfigService` for typed access to env vars; validate configuration at startup so the app fails fast on missing/invalid settings.
