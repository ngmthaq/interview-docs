# Quản lý state lớn thế nào?

- Local state
- Context
- Redux / Zustand / Jotai
- Khi nào không dùng Redux?

## Chi tiết câu trả lời

State management strategies.

### Local state

- useState cho component-specific state.
- Lifting up nếu share.

### Context

- Share state across tree without props drilling.
- useContext + useReducer cho complex state.

### Redux / Zustand / Jotai

- Global state management.
- Redux: Predictable, devtools.
- Zustand/Jotai: Lightweight alternatives.

### Khi nào không dùng Redux?

- App nhỏ, local state đủ.
- Overkill cho simple apps.
- Learning curve cao.

Start simple, scale up khi cần.
