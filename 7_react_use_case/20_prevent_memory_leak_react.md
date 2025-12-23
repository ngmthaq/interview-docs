# Prevent memory leak trong React

- Cleanup useEffect
- Cancel async task
- Avoid stale closure

## Chi tiết câu trả lời

Prevent memory leaks.

### Cleanup useEffect

- Return cleanup function.
- Clear timers, subscriptions.

### Cancel async task

- AbortController cancel requests.
- Prevent state updates on unmount.

### Avoid stale closure

- useCallback cho stable references.
- Careful với closures in effects.

Essential cho long-running apps.
