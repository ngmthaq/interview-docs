# Fetch API khi component mount

- `onMounted`
- AbortController
- Loading / error state

## Chi tiết câu trả lời

Data fetching on mount.

### `onMounted`

- Fetch after DOM ready.
- Avoid SSR issues.

### AbortController

- Cancel on unmount.
- Prevent memory leaks.

### Loading / error state

- UX feedback.
- Handle errors gracefully.

Composition API for clean logic.
