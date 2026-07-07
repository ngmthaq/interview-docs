# 28. How do you generate API documentation? (Senior)

Nest's **`@nestjs/swagger`** auto-generates **OpenAPI (Swagger)** docs from your controllers, DTOs, and decorators.

```ts
// main.ts
const config = new DocumentBuilder().setTitle("Cats API").setVersion("1.0").addBearerAuth().build();

const document = SwaggerModule.createDocument(app, config);
SwaggerModule.setup("api/docs", app, document); // served at /api/docs
```

**Enrich the schema with decorators:**

```ts
export class CreateCatDto {
  @ApiProperty({ example: "Whiskers" })
  name: string;

  @ApiProperty({ minimum: 0, example: 3 })
  age: number;
}

@ApiTags("cats")
@Controller("cats")
export class CatsController {
  @ApiOperation({ summary: "Create a cat" })
  @ApiResponse({ status: 201, type: Cat })
  @Post()
  create(@Body() dto: CreateCatDto) { ... }
}
```

**Bonus:** the **CLI plugin** infers many `@ApiProperty` annotations automatically from types, reducing boilerplate.

**Key point:** `@nestjs/swagger` builds interactive OpenAPI docs from your existing decorators and DTOs; enrich with `@ApiProperty`/`@ApiOperation`/`@ApiTags`, enable the CLI plugin to auto-infer schemas, and serve the UI at a route like `/api/docs`.
