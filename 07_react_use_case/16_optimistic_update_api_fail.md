# Optimistic update nhưng API fail

- Rollback state
- Toast / notification
- Retry

## Chi tiết câu trả lời

Handle optimistic update failures.

### Rollback state

- Revert to previous state.
- Show error.

### Toast / notification

- Notify user of failure.
- Explain what happened.

### Retry

- Allow user retry.
- Automatic retry for transient errors.

Maintain good UX on failures.
