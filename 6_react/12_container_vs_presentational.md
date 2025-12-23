# Container vs Presentational Component

- Container: logic, data
- Presentational: UI
- Hook hiện đại thay thế pattern cũ

## Chi tiết câu trả lời

Separation of concerns trong components.

### Container Component

- Handle logic, data fetching.
- Connect to state management.
- Pass data xuống presentational.

### Presentational Component

- Receive props, render UI.
- Stateless, reusable.
- Dumb components.

### Hook thay thế

- Hooks allow logic in presentational components.
- Custom hooks extract logic.
- No need separate container files.

Modern React: Functional components + hooks unify patterns.
