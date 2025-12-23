# Custom Hook dùng khi nào?

- Tách logic dùng chung
- Không render UI
- Quy tắc đặt tên `useXxx`

## Chi tiết câu trả lời

Custom hooks tái sử dụng logic.

### Tách logic dùng chung

- Extract stateful logic từ components.
- Ví dụ: useLocalStorage, useFetch.
- Components focus trên UI.

### Không render UI

- Hooks chỉ return values/functions, không JSX.
- UI logic ở components.

### Quy tắc đặt tên

- Bắt đầu bằng "use" (useCounter, useApi).
- ESLint rule enforce.
- Dễ identify custom hooks.

Custom hooks follow same rules như built-in hooks.
