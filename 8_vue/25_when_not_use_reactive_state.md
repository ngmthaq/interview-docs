# Khi nào không nên dùng reactive state?

- Derived state
- Computed thay thế
- Tránh over-reactivity

## Chi tiết câu trả lời

When not to use reactive state.

### Derived state

- Compute from existing state.
- No need separate reactive.

### Computed thay thế

- For derived values.
- Cached, efficient.

### Tránh over-reactivity

- Too many reactive objects slow.
- Use plain objects nếu không need reactivity.

Minimize reactive state.
