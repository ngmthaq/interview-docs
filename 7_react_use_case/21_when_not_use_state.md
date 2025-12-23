# Khi nào không nên dùng state?

- Derived state
- Computed value
- useMemo thay thế

## Chi tiết câu trả lời

When not to use state.

### Derived state

- Compute from props/state existing.
- No need separate state.

### Computed value

- Expensive computations: useMemo.
- Not state.

### useMemo thay thế

- For values depend on props/state.
- Avoid unnecessary state.

Minimize state usage.
