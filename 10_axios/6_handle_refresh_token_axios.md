## Refresh token mà KHÔNG huỷ flow gọi API cũ như thế nào?

### Vấn đề

- Nhiều request dùng **access token cũ**
- Backend trả **401 (token hết hạn)**
- Nếu refresh token **sai cách**:
  - Huỷ request cũ
  - Gọi refresh nhiều lần
  - Race condition, logout ngẫu nhiên

👉 Mục tiêu:

> **Refresh token xong → request cũ tiếp tục chạy lại, user không biết gì xảy ra**

---

## Giải pháp chuẩn: Queue + Retry request cũ

### Ý tưởng cốt lõi

1. Khi gặp **401**:
   - KHÔNG reject request ngay
2. Nếu **đang refresh token**:
   - Cho request **chờ trong queue**
3. Refresh token **chỉ 1 lần**
4. Khi refresh xong:
   - Gắn token mới
   - **Retry lại toàn bộ request cũ**

---

## Flow chuẩn

1. Request A, B, C → cùng lúc → 401
2. A trigger refresh token
3. B, C **đứng chờ**
4. Refresh token thành công
5. A, B, C **được retry với token mới**
6. User không bị logout, không reload page

---

## Triển khai bằng Axios (pseudo-code)

### Biến dùng chung

    let isRefreshing = false
    let failedQueue = []

    function processQueue(error, token = null) {
      failedQueue.forEach(promise => {
        if (error) {
          promise.reject(error)
        } else {
          promise.resolve(token)
        }
      })
      failedQueue = []
    }

---

### Response interceptor

    api.interceptors.response.use(
      response => response,
      async error => {
        const originalRequest = error.config

        if (error.response?.status === 401 && !originalRequest._retry) {
          originalRequest._retry = true

          if (isRefreshing) {
            return new Promise((resolve, reject) => {
              failedQueue.push({ resolve, reject })
            }).then(token => {
              originalRequest.headers.Authorization = `Bearer ${token}`
              return api(originalRequest)
            })
          }

          isRefreshing = true

          try {
            const newToken = await refreshToken()

            setAccessToken(newToken)
            processQueue(null, newToken)

            originalRequest.headers.Authorization = `Bearer ${newToken}`
            return api(originalRequest)
          } catch (refreshError) {
            processQueue(refreshError, null)
            logout()
            return Promise.reject(refreshError)
          } finally {
            isRefreshing = false
          }
        }

        return Promise.reject(error)
      }
    )

---

## Vì sao flow này KHÔNG huỷ request cũ?

- Request cũ:
  - Không reject ngay
  - Được wrap trong Promise
- Khi refresh xong:
  - Promise resolve
  - Request **được gọi lại**

➡️ Với caller:

- Không biết refresh xảy ra
- Chỉ thấy request thành công

---

## Những lỗi phổ biến cần tránh

❌ Refresh token cho **mỗi request 401**  
❌ Reject request cũ ngay khi gặp 401  
❌ Không đánh dấu `_retry` → infinite loop  
❌ Refresh token trong request interceptor

---

## Khi nào NÊN huỷ flow cũ?

- Refresh token cũng **hết hạn**
- Backend trả **401 cho refresh API**
- Token bị revoke

👉 Khi đó:

- Clear auth state
- Redirect login

---

## Câu trả lời chuẩn khi phỏng vấn

> “Không huỷ request cũ khi refresh token.  
> Tôi dùng queue để giữ các request bị 401, chỉ refresh token một lần,  
> sau đó retry lại toàn bộ request cũ với token mới.  
> Cách này tránh race condition và giữ UX liền mạch.”

---

## Tóm tắt ngắn gọn

- ✅ 1 refresh token tại 1 thời điểm
- ✅ Request cũ được retry, không bị drop
- ✅ Không race condition
- ✅ UX mượt

> Đây là **pattern bắt buộc** cho app production dùng Axios + JWT.
