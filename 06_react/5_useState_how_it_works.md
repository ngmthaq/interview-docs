# useState hoạt động thế nào?

- Async update
- Batch update
- Functional update khi phụ thuộc state cũ

## Chi tiết câu trả lời

useState hook cơ bản.

### Async update

- setState không update state ngay lập tức.
- React batch updates để optimize performance.
- State update trong event handlers là async.

### Batch update

- Multiple setState trong cùng event batch thành một render.
- Giảm unnecessary re-renders.

### Functional update

- setState(prev => prev + 1) khi update phụ thuộc state cũ.
- Đảm bảo correct value trong async updates.
- Tránh stale closures.

useState return [state, setState], initial value hoặc lazy initial.
