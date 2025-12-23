# Một form lớn (20–30 field) bị lag khi gõ

- Controlled vs uncontrolled
- react-hook-form
- useRef thay vì useState cho input

## Chi tiết câu trả lời

Optimize large forms tránh lag.

### Controlled vs uncontrolled

- Controlled: State update mỗi keystroke → lag.
- Uncontrolled: DOM manage, access via ref.
- Uncontrolled tốt hơn cho performance.

### react-hook-form

- Optimized form library.
- Uncontrolled internally, controlled API.
- Less re-renders, built-in validation.

### useRef thay vì useState

- useRef không trigger re-render.
- Access value trực tiếp.
- Nhưng lose controlled benefits.

Use react-hook-form cho large forms.
