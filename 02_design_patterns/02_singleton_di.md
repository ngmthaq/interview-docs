# Singleton & Dependency Injection (DI) trong NestJS

Tài liệu này cung cấp cái nhìn **bao quát – từ bản chất đến cách NestJS triển khai** về **Singleton Pattern** và **Dependency Injection (DI)**, tập trung vào tư duy kiến trúc và áp dụng thực tế.

---

## 1. Khái niệm cốt lõi

### Singleton Pattern là gì?

Singleton là **một chiến lược vòng đời (lifecycle strategy)** đảm bảo **chỉ tồn tại duy nhất một instance** của một class trong suốt vòng đời ứng dụng và được **tái sử dụng ở mọi nơi**.

**Dùng khi**:

- Logger, Cache, DB connection pool, Config
- Client của SDK bên thứ ba

**Không dùng khi**:

- Có state theo request/user
- Logic dễ gây race condition (race condition là một lỗi xảy ra khi nhiều luồng (hoặc nhiều tác vụ bất đồng bộ) cùng truy cập và thay đổi một tài nguyên dùng chung, và kết quả cuối cùng phụ thuộc vào thứ tự thực thi, thứ tự này không được kiểm soát.)

---

### Dependency Injection (DI) là gì?

DI là **cơ chế** để:

- Tạo instance
- Quản lý phụ thuộc (dependency graph)
- Cấp phát (inject) instance vào nơi cần dùng

DI giúp:

- Giảm coupling
- Dễ test, dễ thay thế implementation
- Tuân thủ SOLID (đặc biệt là DIP)

---

## 2. Mối quan hệ giữa Singleton và DI

- **Singleton trả lời**: Có bao nhiêu instance?
- **DI trả lời**: Ai tạo và ai cấp instance?

Trong NestJS:

> **Singleton không được code thủ công** (không `getInstance()`),
> mà **được DI container quản lý**.

➡️ **DI chính là “Singleton Manager”**.

---

## 3. DI Container hoạt động như thế nào?

### Mô hình đơn giản hóa

DI container duy trì một **registry (Map)**:

- **Key**: token (class / string / symbol)
- **Value**: provider wrapper (metadata + instance)

Với scope mặc định (`DEFAULT`):

- Nếu **chưa có instance** → tạo mới, lưu lại
- Nếu **đã có** → trả về instance cũ

➡️ Đây chính là Singleton.

---

## 4. Provider & Scope trong NestJS

### Scope mặc định (Singleton)

```ts
@Injectable()
export class LoggerService {}
```

- Tạo 1 lần khi app bootstrap
- Dùng chung toàn app

### Request scope

```ts
@Injectable({ scope: Scope.REQUEST })
export class RequestContextService {}
```

- Mỗi request 1 instance
- Không còn là Singleton

### Transient scope

```ts
@Injectable({ scope: Scope.TRANSIENT })
export class HelperService {}
```

- Mỗi lần inject → instance mới

---

## 5. Lifecycle Management (Quản lý vòng đời)

NestJS không chỉ tạo instance, mà còn **quản lý vòng đời** thông qua lifecycle hooks.

### Các hook quan trọng

| Hook                        | Thời điểm gọi                           |
| --------------------------- | --------------------------------------- |
| `onModuleInit`              | Sau khi provider được tạo & inject xong |
| `onModuleDestroy`           | Khi app shutdown                        |
| `beforeApplicationShutdown` | Nhận tín hiệu SIGTERM                   |

---

### Ví dụ chuẩn

```ts
@Injectable()
export class PrismaService implements OnModuleInit, OnModuleDestroy {
  async onModuleInit() {
    await this.$connect();
  }

  async onModuleDestroy() {
    await this.$disconnect();
  }
}
```

**Lưu ý**:

- Không đặt logic nặng trong constructor
- Dùng lifecycle hook để đảm bảo thứ tự và testability

---

## 6. Thứ tự khởi tạo (Dependency Order)

Nếu:

```
A phụ thuộc B
```

Thứ tự init:

```
B.onModuleInit()
A.onModuleInit()
```

NestJS đảm bảo **dependency luôn sẵn sàng trước**.

---

## 7. So sánh Singleton truyền thống vs DI-managed Singleton

| Tiêu chí          | Singleton truyền thống | DI (NestJS)  |
| ----------------- | ---------------------- | ------------ |
| Quản lý lifecycle | Class tự quản          | DI container |
| Test / Mock       | Khó                    | Dễ           |
| Thay thế impl     | Khó                    | Dễ           |
| Scope linh hoạt   | Không                  | Có           |
| Phù hợp NestJS    | Không                  | Có           |

---

## 8. Anti-pattern cần tránh

❌ Dùng `static` để giữ state

```ts
class BadService {
  static value = 0;
}
```

❌ Singleton chứa state theo user

```ts
@Injectable()
export class SessionService {
  currentUserId: string; // nguy hiểm
}
```

❌ Logic init trong constructor

```ts
constructor() {
  this.connectDb(); // sai
}
```

---

## 9. Best Practices

- Để DI container quản lý Singleton
- Provider mặc định nên **stateless**
- Dùng `onModuleInit` cho init logic
- Chỉ dùng Request scope khi thật sự cần
- Tránh `static` và `getInstance()`

---

## 10. Tóm tắt một câu

> **Trong NestJS, Singleton không phải là pattern bạn code,
> mà là lifecycle được DI container quản lý.**

DI vừa là **Singleton Manager**, vừa là **Lifecycle Orchestrator**.

---
