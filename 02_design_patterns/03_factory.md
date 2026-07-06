# Factory Pattern – Tóm tắt ngắn gọn

## 1. Factory Pattern là gì?

**Factory Pattern** là pattern tạo object, trong đó **việc khởi tạo instance được tách khỏi nơi sử dụng**.

👉 Client **không cần biết** object được tạo như thế nào, chỉ cần dùng kết quả.

---

## 2. Khi nào dùng Factory?

- Có **nhiều loại object** cùng vai trò
- Logic tạo object **phức tạp / có điều kiện**
- Muốn tuân **OCP + DIP**

---

## 3. Factory Pattern cơ bản

### Ví dụ đơn giản

```ts
interface Payment {
  pay(amount: number): void;
}

class PaypalPayment implements Payment {}
class StripePayment implements Payment {}

class PaymentFactory {
  static create(type: string): Payment {
    if (type === 'paypal') return new PaypalPayment();
    if (type === 'stripe') return new StripePayment();

    throw new Error('Unsupported payment');
  }
}
```

Client:

```ts
const payment = PaymentFactory.create('paypal');
payment.pay(100);
```

---

## 4. Factory vs Không dùng Factory

❌ Không dùng Factory:

- `new` rải rác khắp nơi
- Khó thay đổi, khó test

✅ Dùng Factory:

- Một nơi duy nhất tạo object
- Dễ mở rộng, dễ mock

---

## 5. Factory Pattern trong NestJS

### Factory Provider (chuẩn NestJS)

```ts
{
  provide: 'PAYMENT',
  useFactory: () => {
    return new PaypalPayment();
  },
}
```

Inject:

```ts
constructor(@Inject('PAYMENT') private payment: Payment) {}
```

👉 Kết hợp **DI + Factory**

---

## 6. Factory vs Strategy

| Factory                | Strategy                   |
| ---------------------- | -------------------------- |
| Quyết định tạo object  | Quyết định hành vi runtime |
| Tập trung vào khởi tạo | Tập trung vào logic        |

➡️ Thường dùng **Factory để chọn Strategy**

---

## 7. Ưu / Nhược điểm

### Ưu điểm

- Giảm coupling
- Tuân SOLID (OCP, DIP)
- Dễ test

### Nhược điểm

- Tăng số class
- Overkill với bài toán nhỏ

---

## 8. Ghi nhớ nhanh

```
Factory = Ẩn logic tạo object
Dùng khi: nhiều loại + nhiều điều kiện
NestJS: useFactory + DI
```

---
