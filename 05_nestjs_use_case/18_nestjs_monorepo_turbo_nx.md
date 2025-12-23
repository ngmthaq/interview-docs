# NestJS trong monorepo (Turbo / Nx)

- Shared library
- Versioning
- Boundary giữa app và lib

## Chi tiết câu trả lời

NestJS in monorepo.

### Shared library

- Extract common code thành libs.
- Use Nx libs cho shared modules/services.
- Build và test independently.

### Versioning

- Use workspace versioning.
- Tag releases cho libs.
- Dependency management.

### Boundary giữa app và lib

- Clear contracts giữa apps và libs.
- Libs không depend on apps.
- Use interfaces cho decoupling.

Leverage Nx cho build orchestration.