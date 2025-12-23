# React Router hoạt động thế nào?

- useParams
- useNavigate
- Protected route

## Chi tiết câu trả lời

React Router cho routing.

### useParams

- Extract dynamic params từ URL.
- useParams() return object {id: '123'}.

### useNavigate

- Programmatic navigation.
- navigate('/path'), navigate(-1).

### Protected route

- Component check auth before render.
- Redirect nếu unauthorized.
- Use context hoặc auth hook.

React Router v6 declarative routing.
