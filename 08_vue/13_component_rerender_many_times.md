# Component re-render nhiều lần

- Reactive dependency
- Avoid deep watch
- Computed tối ưu hơn watch

## Chi tiết câu trả lời

Prevent excessive re-renders.

### Reactive dependency

- Only track needed properties.
- Avoid unnecessary reactivity.

### Avoid deep watch

- Deep watch expensive.
- Use shallow watch nếu possible.

### Computed tối ưu hơn watch

- Computed cached.
- Watch run every change.

Profile và optimize carefully.
