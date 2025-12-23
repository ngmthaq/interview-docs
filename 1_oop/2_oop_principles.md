## 4 tính chất của OOP (mô tả rõ + gắn với code)

Ví dụ minh họa bằng TypeScript (tư duy tương tự Java / C#).

---

## 1. Encapsulation (Đóng gói)

**Ý nghĩa**

- Ẩn dữ liệu bên trong object
- Ngăn truy cập trực tiếp vào trạng thái nội tại
- Object tự bảo vệ invariant của nó

**Ví dụ**

    class BankAccount {
      private balance: number = 0;

      deposit(amount: number) {
        if (amount <= 0) {
          throw new Error('Invalid amount');
        }
        this.balance += amount;
      }

      getBalance() {
        return this.balance;
      }
    }

**Giải thích**

- `balance` không thể bị sửa trực tiếp từ bên ngoài
- Mọi thay đổi đều phải thông qua method có kiểm soát

---

## 2. Abstraction (Trừu tượng)

**Ý nghĩa**

- Chỉ quan tâm hệ thống làm được gì
- Không quan tâm chi tiết triển khai
- Giảm phụ thuộc giữa các module

**Ví dụ**

    interface PaymentGateway {
      pay(amount: number): void;
    }

**Các implementation**

    class PaypalPayment implements PaymentGateway {
      pay(amount: number) {
        console.log('Pay by PayPal');
      }
    }

    class CreditCardPayment implements PaymentGateway {
      pay(amount: number) {
        console.log('Pay by Credit Card');
      }
    }

**Sử dụng abstraction**

    function checkout(gateway: PaymentGateway) {
      gateway.pay(100);
    }

**Lợi ích**

- `checkout` không quan tâm payment cụ thể
- Thêm payment mới **không sửa code cũ**
- Tuân thủ Open/Closed Principle

---

## 3. Inheritance (Kế thừa)

**Ý nghĩa**

- Class con kế thừa hành vi từ class cha
- Thể hiện quan hệ IS-A

**Ví dụ**

    abstract class Employee {
      abstract getSalary(): number;
    }

    class FullTimeEmployee extends Employee {
      getSalary(): number {
        return 1000;
      }
    }

**Lưu ý**

- Chỉ dùng khi có quan hệ IS-A rõ ràng
- Lạm dụng gây coupling cao và khó bảo trì

---

## 4. Polymorphism (Đa hình)

**Ý nghĩa**

- Cùng một interface, nhiều cách triển khai
- Quyết định hành vi tại runtime
- Thay thế if/else

**Ví dụ**

    class CreditCardPayment implements PaymentGateway {
      pay(amount: number) {
        console.log(`Pay ${amount} by credit card`);
      }
    }

    class PaypalPayment implements PaymentGateway {
      pay(amount: number) {
        console.log(`Pay ${amount} by PayPal`);
      }
    }

Sử dụng:

    const gateway: PaymentGateway = new PaypalPayment();
    gateway.pay(100);

**Giải thích**

- Không cần kiểm tra loại payment
- Thêm phương thức thanh toán mới không sửa code cũ

---

## Tổng kết

| Tính chất     | Mục đích chính    |
| ------------- | ----------------- |
| Encapsulation | Bảo vệ trạng thái |
| Abstraction   | Giảm phụ thuộc    |
| Inheritance   | Tái sử dụng code  |
| Polymorphism  | Mở rộng hệ thống  |

> OOP hiệu quả là dùng đúng tính chất, đúng ngữ cảnh, không phải dùng càng nhiều càng tốt.
