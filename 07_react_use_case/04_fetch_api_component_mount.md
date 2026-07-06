# Fetch API khi component mount

- useEffect
- Cleanup request
- Loading / error state

## Chi tiết câu trả lời

Fetch data on mount.

### useEffect

- useEffect(() => fetch(), []) run on mount.
- Dependency array empty.

### Cleanup request

- Return cleanup function cancel request.
- Prevent state update on unmounted component.

### Loading / error state

- useState cho loading, error.
- Show loading UI, handle errors.

Essential cho good UX.
