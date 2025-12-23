# SOLID – Tóm tắt ngắn gọn

## SOLID là gì?

**SOLID** là 5 nguyên lý thiết kế OOP giúp code **dễ bảo trì, dễ mở rộng, dễ test**. Đặc biệt phù hợp với **NestJS** nhờ Dependency Injection.

---

## 1. S – Single Responsibility Principle (SRP)

**Một class chỉ làm một việc.**

- Mỗi class chỉ có **một lý do để thay đổi**
- Tránh God Class

Ví dụ:

- Controller: xử lý HTTP
- Service: business logic
- Repository: data access

---

## 2. O – Open / Closed Principle (OCP)

**Mở để mở rộng, đóng để sửa.**

- Thêm feature bằng code mới
- Không sửa code cũ đã ổn định

→ Dùng `interface`, `strategy`, `provider`

---

## 3. L – Liskov Substitution Principle (LSP)

**Class con thay thế được class cha.**

- Không override làm thay đổi hành vi
- Không throw error phá contract

---

## 4. I – Interface Segregation Principle (ISP)

**Interface nhỏ, chuyên biệt.**

- Không ép class implement method không dùng
- Chia interface theo hành vi

---

## 5. D – Dependency Inversion Principle (DIP)

**Phụ thuộc abstraction, không phụ thuộc implementation.**

- Không `new` dependency trong class
- Dùng DI Container (NestJS)

---

## SOLID trong NestJS (nhớ nhanh)

- SRP: Controller / Service / Repository
- OCP: Provider + Strategy
- LSP: Abstraction đúng nghĩa
- ISP: Interface nhỏ
- DIP: Dependency Injection

---

## Ghi nhớ 1 dòng

```
S – 1 class = 1 trách nhiệm
O – Mở rộng, không sửa
L – Thay thế được
I – Interface nhỏ
D – Phụ thuộc abstraction
```

---
