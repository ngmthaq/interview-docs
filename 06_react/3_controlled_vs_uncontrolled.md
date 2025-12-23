# Controlled vs Uncontrolled Component

- Controlled: React kiểm soát value
- Uncontrolled: DOM tự quản
- Khi nào dùng mỗi loại?

## Chi tiết câu trả lời

Controlled và uncontrolled components trong form handling.

### Controlled Component

- React state quản lý value của input.
- onChange handler update state.
- Predictable, dễ validate, test.

### Uncontrolled Component

- DOM manage value internally.
- Use ref để access value khi cần.
- Simple cho forms đơn giản, không cần validation phức tạp.

### Khi nào dùng?

- **Controlled**: Validation real-time, dynamic forms, state-dependent logic.
- **Uncontrolled**: Simple forms, integrate với non-React code, performance-critical (ít re-renders).

React khuyến khích controlled cho consistency.
