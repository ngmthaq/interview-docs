# 12. What is the NestJS request lifecycle order? (Mid)

Understanding the **order** components run in is a common senior interview question. A request flows through:

```
1. Middleware
2. Guards
3. Interceptors (pre-controller)
4. Pipes
5. Route handler (controller → service)
6. Interceptors (post-controller)
7. Exception filters (if an error is thrown anywhere)
8. Response sent
```

```ts
// Roughly what each stage does:
Middleware   → logging, CORS, raw req/res
Guards       → can this request proceed? (auth)
Interceptor  → start timer, prepare
Pipes        → validate/transform args
Handler      → business logic
Interceptor  → transform response, log duration
Filters      → catch & format any thrown exception
```

**Key points about order:**

- **Guards run before pipes** — auth is checked before expensive validation.
- **Interceptors straddle** the handler (pre and post).
- **Exception filters** catch errors from any stage and shape the error response.
- Enhancers can be **global → controller → method** scoped; global run outermost.

**Key point:** the lifecycle is middleware → guards → interceptors(pre) → pipes → handler → interceptors(post) → exception filters; knowing this order explains why auth (guards) precedes validation (pipes) and how responses/errors get transformed.
