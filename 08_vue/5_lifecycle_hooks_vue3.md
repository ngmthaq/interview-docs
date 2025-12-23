# Lifecycle hooks trong Vue 3

- `setup`
- `onMounted`, `onUpdated`, `onUnmounted`
- Cleanup effect ở đâu?

## Chi tiết câu trả lời

Lifecycle hooks Vue 3 Composition API.

### `setup`

- Entry point cho Composition API.
- Run trước render.
- Return template bindings.

### `onMounted`, `onUpdated`, `onUnmounted`

- `onMounted`: After DOM mounted.
- `onUpdated`: After update.
- `onUnmounted`: Before unmount.

### Cleanup effect ở đâu?

- Trong `onUnmounted`.
- Clear timers, listeners.
- Prevent memory leaks.

Composition API flexible hơn Options API.
