# Hai API gọi song song, API A phụ thuộc API B

- Promise chaining
- useEffect dependency
- Tách effect theo trách nhiệm

## Chi tiết câu trả lời

Handle dependent async operations.

### Promise chaining

- Fetch B, then A with data from B.
- Sequential execution.

### useEffect dependency

- Effect run khi dependency change.
- Careful với infinite loops.

### Tách effect theo trách nhiệm

- Separate effects cho each API.
- State manage dependencies.

Ensure correct order và error handling.
