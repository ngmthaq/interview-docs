# Props drilling là gì? Giải pháp?

- Context
- State management library
- Component composition

## Chi tiết câu trả lời

Props drilling problem.

### Props drilling

- Pass props qua nhiều levels components.
- Intermediate components không cần props.
- Code verbose, hard maintain.

### Giải pháp

- **Context**: Provide/consume ở bất kỳ level.
- **State management**: Redux, etc. global access.
- **Composition**: Render props, children as function.

Context cho simple cases, libraries cho complex.
