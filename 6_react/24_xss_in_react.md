# XSS trong React có xảy ra không?

- JSX auto escape
- Nguy hiểm khi dùng `dangerouslySetInnerHTML`

## Chi tiết câu trả lời

Security trong React.

### JSX auto escape

- JSX escape HTML automatically.
- Safe render user input.

### dangerouslySetInnerHTML

- Bypass escaping.
- Risk XSS nếu input untrusted.
- Sanitize input trước dùng.

React secure by default, nhưng careful với raw HTML.
