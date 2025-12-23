# Adapter Design Pattern – Tóm tắt ngắn gọn

## 1. Adapter Pattern là gì?

**Adapter Pattern** dùng để **kết nối hai interface không tương thích** mà **không sửa code gốc**.

👉 Adapter đóng vai trò **bộ chuyển đổi (translator)** giữa client và hệ thống bên ngoài.

---

## 2. Khi nào dùng Adapter?

- Tích hợp **third-party / legacy system**
- Interface bên ngoài **không khớp** với interface nội bộ
- Không thể (hoặc không nên) sửa code gốc

---

## 3. Cấu trúc cơ bản

- **Target**: interface mà client mong đợi
- **Adaptee**: class hiện có (không tương thích)
- **Adapter**: implement Target, wrap Adaptee

---

## 4. Ví dụ đơn giản (TypeScript)

```ts
// Target
interface Payment {
  pay(amount: number): void;
}

// Adaptee (third-party)
class PaypalSDK {
  sendMoney(value: number) {}
}

// Adapter
class PaypalAdapter implements Payment {
  constructor(private paypal: PaypalSDK) {}

  pay(amount: number) {
    this.paypal.sendMoney(amount);
  }
}
```

Sử dụng:

```ts
const payment: Payment = new PaypalAdapter(new PaypalSDK());
payment.pay(100);
```

---

## 5. Adapter vs Không dùng Adapter

❌ Không dùng Adapter:

- Code phụ thuộc trực tiếp SDK ngoài
- Khó thay thế, khó test

✅ Dùng Adapter:

- Code chỉ phụ thuộc interface nội bộ
- Thay SDK không ảnh hưởng hệ thống

---

## 6. Adapter trong NestJS

Thường dùng khi:

- Gọi API bên thứ ba
- Wrap SDK (payment, SMS, email)

Ví dụ khái niệm:

- `HttpService` bọc Axios
- Custom service bọc Firebase / AWS SDK

👉 Adapter giúp tuân **DIP + OCP**

---

## 7. Adapter vs Facade

| Adapter                      | Facade                 |
| ---------------------------- | ---------------------- |
| Chuyển interface             | Đơn giản hóa interface |
| Giải quyết không tương thích | Che độ phức tạp        |

---

## 8. Ưu / Nhược điểm

### Ưu điểm

- Không sửa code gốc
- Giảm coupling
- Dễ test, dễ thay thế

### Nhược điểm

- Thêm layer trung gian
- Có thể nhiều adapter nếu nhiều SDK

---

## 9. Ghi nhớ nhanh

```
Adapter = Chuyển interface
Dùng khi tích hợp hệ ngoài
Không sửa code gốc
```

---
