# Fetch data trong React thế nào cho đúng?

- useEffect
- AbortController
- Loading / error state

## Chi tiết câu trả lời

Data fetching best practices.

### useEffect

- Fetch trong useEffect với dependency.
- Cleanup để cancel nếu component unmount.

### AbortController

- Cancel requests khi component unmount.
- Prevent state updates on unmounted component.

### Loading / error state

- useState cho loading, error.
- Show loading UI, error messages.
- Handle race conditions.

Use libraries như React Query cho advanced features.
