# MVC & Repository Pattern – Tóm tắt ngắn gọn

## 1. MVC là gì?

**MVC (Model – View – Controller)** là pattern tổ chức ứng dụng, tách rõ trách nhiệm:

- **Model**: dữ liệu + nghiệp vụ
- **View**: hiển thị (UI hoặc JSON)
- **Controller**: nhận request, điều phối

👉 Mục tiêu: **tách biệt concern, dễ bảo trì**.

---

## 2. MVC trong Backend (NestJS)

Trong NestJS (backend API), MVC được hiểu theo cách thực dụng:

- **Controller** → nhận HTTP request
- **Service (Model)** → business logic
- **View** → JSON response (hoặc template nếu SSR)

```text
Request → Controller → Service → Repository → DB
```

---

## 3. Repository Pattern là gì?

**Repository Pattern** tách riêng **logic truy cập dữ liệu** ra khỏi business logic.

👉 Service **không biết DB là gì**, chỉ biết Repository.

---

## 4. Khi nào dùng Repository?

- Muốn đổi DB mà không ảnh hưởng business logic
- Muốn test service dễ hơn (mock repository)
- Muốn code sạch, tuân **SRP + DIP**

---

## 5. Cấu trúc MVC + Repository

- Controller: HTTP, validate input
- Service: nghiệp vụ chính
- Repository: query DB
- Entity/Model: mapping dữ liệu

---

## 6. Ví dụ đơn giản (NestJS)

### Repository

```ts
export interface UserRepository {
  findById(id: string): Promise<User>;
}
```

```ts
@Injectable()
export class UserRepositoryImpl implements UserRepository {
  findById(id: string) {
    // query DB
  }
}
```

### Service (Model)

```ts
@Injectable()
export class UserService {
  constructor(private repo: UserRepository) {}

  getUser(id: string) {
    return this.repo.findById(id);
  }
}
```

### Controller

```ts
@Controller('users')
export class UserController {
  constructor(private service: UserService) {}

  @Get(':id')
  getUser(@Param('id') id: string) {
    return this.service.getUser(id);
  }
}
```

---

## 7. MVC + Repository mang lại gì?

- Controller mỏng
- Service tập trung nghiệp vụ
- Repository cô lập DB

➡️ Code **dễ test – dễ mở rộng – dễ thay DB**

---

## 8. MVC vs Clean Architecture (rất ngắn)

- MVC: đơn giản, dễ dùng
- MVC + Repository: đủ cho đa số project
- Clean Architecture: cho hệ lớn, phức tạp

---

## 9. Ghi nhớ nhanh

```
MVC = Tách UI / Logic / Điều phối
Repository = Tách DB khỏi business
NestJS = MVC + Repository mặc định
```

---
