# Quản lý form lớn thế nào?

- Controlled input
- react-hook-form / Formik
- Performance trade-off

## Chi tiết câu trả lời

Form management trong React.

### Controlled input

- State manage all inputs.
- onChange update state.
- Easy validation, nhưng re-render nhiều.

### react-hook-form / Formik

- Uncontrolled internally, controlled API.
- Less re-renders, better performance.
- Built-in validation, error handling.

### Performance trade-off

- Controlled: Predictable, nhưng slow cho large forms.
- Libraries: Optimized, nhưng learning curve.

Choose based on form complexity.
