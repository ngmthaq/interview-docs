# Memory leak trong Vue app

- Cleanup trong `onUnmounted`
- Clear timer / listener
- Cancel request

## Chi tiết câu trả lời

Memory leaks in Vue.

### Cleanup trong `onUnmounted`

- Remove listeners.
- Clear intervals.

### Clear timer / listener

- Explicit cleanup.
- Prevent accumulation.

### Cancel request

- AbortController.
- Avoid state updates.

Always cleanup effects.
