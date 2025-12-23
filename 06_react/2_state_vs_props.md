# State vs Props khác nhau thế nào?

- Props: từ cha → con, immutable
- State: internal, có thể thay đổi
- Khi nào nâng state lên (lifting state up)?

## Chi tiết câu trả lời

State và props là hai khái niệm cốt lõi trong React.

### Props

- Dữ liệu truyền từ component cha xuống con.
- Immutable: Con không thể thay đổi props trực tiếp.
- Sử dụng để customize component behavior.

### State

- Dữ liệu internal của component.
- Mutable: Có thể thay đổi bằng setState/useState.
- Khi state thay đổi, component re-render.

### Khi nào nâng state lên?

- Khi nhiều components cần share state.
- Nâng lên component cha chung gần nhất.
- Sử dụng props để truyền xuống.
- Ví dụ: Form với multiple inputs share validation state.

Lifting state up giúp manage state centralized.
