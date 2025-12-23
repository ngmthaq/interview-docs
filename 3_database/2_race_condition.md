# Tài liệu thiết kế kỹ thuật

## Xử lý đồng thời 2 API lấy cùng 1 item (chỉ còn 1 tồn kho)

### Công nghệ sử dụng

- Backend: NestJS
- ORM: TypeORM
- Database: MySQL / PostgreSQL
- Kiến trúc: Monolith / API-based

---

## 1. Mô tả bài toán

Hệ thống cung cấp API tạo đơn hàng (`Create Order`).  
Mỗi item có số lượng tồn kho (stock) được lưu trong database.

**Tình huống:**

- Có **2 request API gửi đồng thời**
- Cùng `itemId`
- Item chỉ còn **1 đơn vị tồn kho**

**Rủi ro nếu không xử lý đúng:**

- Tạo ra **2 order cho cùng 1 item**
- Stock bị trừ sai (âm)
- Gây oversell và sai lệch dữ liệu

---

## 2. Nguyên nhân gốc rễ (Root Cause)

Đây là bài toán **Race Condition**.

### Luồng xử lý sai phổ biến

1. Request A đọc stock = 1
2. Request B đọc stock = 1
3. Request A cập nhật stock → 0
4. Request B cập nhật stock → -1

**Nguyên nhân:**

- Không sử dụng transaction
- Không khóa dữ liệu (lock)
- Kiểm tra logic ở application-level thay vì database-level

---

## 3. Mục tiêu thiết kế

- Chỉ **1 request được phép thành công**
- Request còn lại **fail có kiểm soát**
- Không oversell
- Không deadlock
- Đảm bảo toàn vẹn dữ liệu trong môi trường production

---

## 4. Giải pháp được lựa chọn

### Transaction + Pessimistic Lock (Row-level locking)

**Nguyên lý:**

- Khóa row của item ngay khi đọc dữ liệu
- Chỉ cho phép **1 transaction** thao tác trên item tại một thời điểm
- Các request còn lại phải chờ hoặc bị timeout

**Lý do chọn giải pháp này:**

- Độ chính xác tuyệt đối
- Database đảm bảo tính toàn vẹn
- Phù hợp cho tài nguyên có xung đột cao (stock, booking, order)

---

## 5. Luồng xử lý chi tiết

1. Client gọi `POST /orders`
2. Backend bắt đầu transaction
3. Lock item bằng `SELECT ... FOR UPDATE`
4. Kiểm tra tồn kho
   - Nếu `stock < 1` → trả lỗi
5. Trừ stock
6. Tạo order
7. Commit transaction

---

## 6. Chi tiết implement (NestJS + TypeORM)

```ts
@Injectable()
export class OrderService {
  constructor(private readonly dataSource: DataSource) {}

  async createOrder(userId: number, itemId: number) {
    return this.dataSource.transaction(async (manager) => {
      const item = await manager
        .createQueryBuilder(Item, 'item')
        .setLock('pessimistic_write')
        .where('item.id = :id', { id: itemId })
        .getOne();

      if (!item) {
        throw new NotFoundException('Không tìm thấy item');
      }

      if (item.stock < 1) {
        throw new ConflictException('Item đã hết hàng');
      }

      item.stock -= 1;
      await manager.save(item);

      const order = manager.create(Order, {
        userId,
        itemId,
        status: 'CONFIRMED',
      });

      await manager.save(order);

      return order;
    });
  }
}
```
