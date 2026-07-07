# 4. What are controllers in NestJS? (Fresher)

**Controllers** handle incoming **requests** and return **responses**. They're classes decorated with **`@Controller()`**, and their methods use HTTP-method decorators to define routes.

```ts
import { Controller, Get, Post, Body, Param, Query } from "@nestjs/common";

@Controller("cats") // base path: /cats
export class CatsController {
  constructor(private readonly catsService: CatsService) {}

  @Get() // GET /cats
  findAll(@Query("limit") limit: string) {
    return this.catsService.findAll(limit);
  }

  @Get(":id") // GET /cats/:id
  findOne(@Param("id") id: string) {
    return this.catsService.findOne(id);
  }

  @Post() // POST /cats
  create(@Body() dto: CreateCatDto) {
    return this.catsService.create(dto);
  }
}
```

**Parameter decorators** extract request data: `@Body()`, `@Param()`, `@Query()`, `@Headers()`, `@Req()`.

**Best practice:** keep controllers **thin** — they should delegate business logic to injected **services**, not contain it.

**Key point:** controllers map routes to handler methods via decorators (`@Get`, `@Post`, `@Param`, `@Body`) and should stay thin, delegating real work to injected services.
