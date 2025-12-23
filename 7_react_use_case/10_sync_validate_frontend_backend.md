# Đồng bộ validate frontend & backend

- Shared schema (Zod / Yup)
- Backend là source of truth

## Chi tiết câu trả lời

Sync validation rules.

### Shared schema

- Define schema in shared package.
- Use Zod/Yup ở both ends.

### Backend là source of truth

- Backend validate strictly.
- Frontend validate cho UX.
- Backend errors override.

Ensure consistency.
