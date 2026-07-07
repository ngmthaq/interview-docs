# 18. How do you implement authentication in NestJS? (Mid)

Nest integrates **Passport** via `@nestjs/passport` and `@nestjs/jwt`. The typical JWT flow uses a strategy + guard.

```ts
// jwt.strategy.ts
@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
  constructor(config: ConfigService) {
    super({
      jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
      secretOrKey: config.get("JWT_SECRET"),
    });
  }
  // return value is attached to req.user
  async validate(payload: { sub: string; email: string }) {
    return { userId: payload.sub, email: payload.email };
  }
}

// login — issue a token
@Injectable()
export class AuthService {
  constructor(private jwt: JwtService) {}
  async login(user: User) {
    return { access_token: this.jwt.sign({ sub: user.id, email: user.email }) };
  }
}

// protect routes with the built-in guard
@UseGuards(AuthGuard("jwt"))
@Get("profile")
getProfile(@Req() req) {
  return req.user;
}
```

**Key point:** use `@nestjs/passport` + `@nestjs/jwt` — define a `JwtStrategy` whose `validate()` populates `req.user`, issue tokens with `JwtService`, and protect routes with `AuthGuard("jwt")`; combine with a roles guard for authorization.
