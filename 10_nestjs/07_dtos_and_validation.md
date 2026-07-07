# 7. What are DTOs and how do you validate them? (Junior)

A **DTO** (Data Transfer Object) defines the **shape of data** crossing a boundary — e.g. a request body. Combined with **`class-validator`** and the **`ValidationPipe`**, Nest validates input automatically.

```ts
import { IsEmail, IsString, MinLength, IsInt, Min, IsOptional } from "class-validator";

export class CreateUserDto {
  @IsString()
  @MinLength(1)
  name: string;

  @IsEmail()
  email: string;

  @IsInt()
  @Min(0)
  @IsOptional()
  age?: number;
}
```

Enable validation globally:

```ts
app.useGlobalPipes(new ValidationPipe({ whitelist: true, transform: true }));
// whitelist strips unknown props; transform coerces types & instantiates the DTO
```

```ts
@Post()
create(@Body() dto: CreateUserDto) { // auto-validated; 400 on failure
  return this.usersService.create(dto);
}
```

**Key point:** DTOs are classes describing expected data; decorate them with `class-validator` rules and enable the `ValidationPipe` (with `whitelist` + `transform`) so Nest validates and sanitizes every request automatically, returning 400 on bad input.
