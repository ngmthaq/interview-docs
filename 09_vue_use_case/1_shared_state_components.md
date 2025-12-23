# Nhiều component cần dùng chung state, bạn xử lý thế nào?

- Lifting state lên cha
- Pinia
- Provide / Inject
- Trade-off giữa local và global state

## Chi tiết câu trả lời

Xử lý shared state trong Vue.

### Lifting state lên cha

- State lên component cha.
- Pass xuống qua props.
- Simple, nhưng prop drilling nếu deep.

### Pinia

- Global state management.
- Reactive, type-safe.
- Best cho complex apps.

### Provide / Inject

- Dependency injection.
- Cha provide, con inject.
- Flexible, nhưng implicit.

### Trade-off giữa local và global state

- Local: simple, isolated.
- Global: shared, nhưng coupling.
- Use local nếu possible, global nếu cần.

Choose based on scope.
