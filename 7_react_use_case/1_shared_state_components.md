# Nhiều component cần dùng chung state, bạn làm thế nào?

- Lifting state up
- Context
- Global state (Redux / Zustand)
- Trade-off giữa coupling và performance

## Chi tiết câu trả lời

Quản lý state dùng chung giữa nhiều components.

### Lifting state up

- Nâng state lên component cha gần nhất.
- Truyền xuống qua props.
- Đơn giản cho tree nhỏ.

### Context

- React Context provide/consume state.
- useContext hook access.
- Tránh props drilling.

### Global state (Redux / Zustand)

- Libraries như Redux, Zustand cho global state.
- Predictable updates, devtools.
- Complex hơn, nhưng scalable.

### Trade-off

- Coupling: Context tăng coupling.
- Performance: Global state có overhead.
- Chọn based on app size và complexity.

Start với lifting, scale to global khi cần.
