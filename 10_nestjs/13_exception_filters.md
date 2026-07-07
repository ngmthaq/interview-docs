# 13. What are exception filters? (Mid)

**Exception filters** catch **unhandled exceptions** and control the **response** sent to the client. Nest ships a global filter that turns `HttpException`s into proper HTTP responses; you can customize it.

```ts
import { ArgumentsHost, Catch, ExceptionFilter, HttpException } from "@nestjs/common";

@Catch(HttpException)
export class HttpExceptionFilter implements ExceptionFilter {
  catch(exception: HttpException, host: ArgumentsHost) {
    const ctx = host.switchToHttp();
    const response = ctx.getResponse();
    const status = exception.getStatus();

    response.status(status).json({
      statusCode: status,
      message: exception.message,
      timestamp: new Date().toISOString(),
    });
  }
}
```

**Built-in exceptions:** `BadRequestException` (400), `UnauthorizedException` (401), `ForbiddenException` (403), `NotFoundException` (404), `ConflictException` (409), etc.

```ts
throw new NotFoundException("User not found"); // → 404 JSON response
```

**Scope:** method, controller, or global (`app.useGlobalFilters`). `@Catch()` with no arg catches everything.

**Key point:** exception filters catch thrown exceptions and format the error response; throw Nest's built-in `HttpException` subclasses for correct status codes, and add a custom `@Catch` filter for consistent, app-wide error shapes.
