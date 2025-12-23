## Nên tạo Axios instance mỗi lần gọi API hay dùng chung?

### Kết luận ngắn gọn

**NÊN dùng chung Axios instance**, **KHÔNG** tạo mới mỗi lần gọi API.

---

## So sánh nhanh

### 1. Tạo Axios instance mỗi lần gọi API

**Ví dụ**

    axios.create({ baseURL: '/api' }).get('/users')

**Nhược điểm**

- Mất interceptor (token, error handling)
- Không chia sẻ config
- Khó maintain, khó debug
- Dễ tạo bug liên quan auth / refresh token

**Chỉ nên dùng khi**

- Cấu hình request **rất đặc biệt**
- One-off request (hiếm gặp)

---

### 2. Dùng chung Axios instance (Best Practice)

**Ví dụ**

    const api = axios.create({
      baseURL: '/api',
      timeout: 10000
    })

**Ưu điểm**

- Centralized config
- Interceptor dùng chung
- Dễ xử lý auth, logging, retry
- Phù hợp dự án vừa & lớn

---

## Khi nào nên dùng NHIỀU instance?

Dùng **nhiều instance**, nhưng **mỗi instance dùng chung cho 1 nhóm API**:

- API khác domain
- Auth khác nhau
- Timeout khác nhau

**Ví dụ**

    export const publicApi = axios.create({ baseURL: '/public' })
    export const privateApi = axios.create({ baseURL: '/private' })

---

## Câu trả lời chuẩn khi phỏng vấn

> “Không nên tạo Axios instance mỗi lần gọi API.  
> Nên dùng một hoặc vài instance dùng chung để quản lý interceptor, auth và error handling tập trung.  
> Chỉ tạo instance riêng khi có cấu hình khác biệt rõ ràng.”

---

## Anti-pattern cần tránh

- `axios.create()` trong component
- Gắn interceptor bên trong function gọi API
- Tạo instance trong mỗi hook

---

## Checklist best practice

- Tạo instance ở tầng infrastructure
- Mỗi domain API một instance
- Interceptor gọn, dễ debug
- Không lạm dụng global state trong interceptor

> **Axios instance là tài nguyên dùng chung, không phải disposable object.**
