# Decorator Design Pattern – Tóm tắt ngắn gọn

## 1. Decorator Pattern là gì?

**Decorator Pattern** cho phép **bổ sung hành vi cho object tại runtime** mà **không sửa code gốc**.

👉 Thay vì kế thừa, ta **bọc (wrap)** object bằng decorator.

---

## 2. Khi nào dùng Decorator?

- Muốn thêm chức năng **linh hoạt** (log, cache, auth, retry)
- Tránh tạo quá nhiều subclass
- Muốn tuân **Open/Closed Principle**

---

## 3. Cấu trúc cơ bản

- **Component**: interface chung
- **ConcreteComponent**: object gốc
- **Decorator**: wrapper giữ reference tới Component
- **ConcreteDecorator**: thêm hành vi

---

## 4. Ví dụ đơn giản (TypeScript)

```ts
interface Notifier {
  send(message: string): void;
}

class EmailNotifier implements Notifier {
  send(message: string) {
    console.log('Send email:', message);
  }
}

class NotifierDecorator implements Notifier {
  constructor(protected notifier: Notifier) {}

  send(message: string) {
    this.notifier.send(message);
  }
}

class SMSDecorator extends NotifierDecorator {
  send(message: string) {
    super.send(message);
    console.log('Send SMS:', message);
  }
}
```

Sử dụng:

```ts
const notifier = new SMSDecorator(new EmailNotifier());
notifier.send('Hello');
```

---

## 5. Decorator vs Inheritance

| Decorator         | Inheritance           |
| ----------------- | --------------------- |
| Linh hoạt runtime | Cố định compile-time  |
| Tránh nổ class    | Dễ tạo nhiều subclass |
| Tuân OCP          | Dễ vi phạm OCP        |

---

## 6. Decorator trong NestJS

NestJS **dùng Decorator cực nhiều**:

- `@Controller()`
- `@Get()` / `@Post()`
- `@UseGuards()`
- `@UseInterceptors()`

👉 Các decorator này **bọc logic** quanh handler gốc.

---

## 7. Decorator (Pattern) vs Decorator (TypeScript)

- **Decorator Pattern**: pattern thiết kế (ý tưởng)
- **TypeScript Decorator**: cú pháp/ngôn ngữ hỗ trợ

NestJS kết hợp **cả hai**.

---

## 8. Ưu / Nhược điểm

### Ưu điểm

- Linh hoạt
- Không sửa code gốc
- Kết hợp được nhiều decorator

### Nhược điểm

- Nhiều wrapper
- Debug khó hơn nếu lạm dụng

---

## 9. Ghi nhớ nhanh

```
Decorator = Bọc thêm hành vi
Không sửa code gốc
Thêm chức năng tại runtime
```

---
