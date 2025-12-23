# Module import quá nhiều, khó kiểm soát

- Shared module
- Global module
- Khi nào KHÔNG nên dùng `@Global()`

## Chi tiết câu trả lời

Manage module dependencies.

### Shared module

- Module chứa common providers.
- Export để other modules import.
- Reduce duplication.

### Global module

- @Global() decorator.
- Available everywhere without import.
- Convenient nhưng có thể gây confusion.

### Khi nào KHÔNG nên dùng @Global()

- Khi dependencies không thực sự global.
- Có thể gây tight coupling.
- Khó track dependencies.

Use sparingly, prefer explicit imports.