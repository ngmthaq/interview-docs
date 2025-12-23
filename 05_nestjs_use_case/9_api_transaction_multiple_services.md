# Một API cần transaction qua nhiều service

- Vì sao không nên tạo transaction trong từng service?
- Transaction ở application layer
- `QueryRunner` / Prisma `$transaction`

## Chi tiết câu trả lời

Transaction spanning multiple services.

### Vì sao không tạo transaction trong từng service?

- Vi phạm Single Responsibility: Service không nên manage transaction.
- Khó control khi services call nhau.
- Có thể nested transactions, phức tạp.

### Transaction ở application layer

- Controller hoặc dedicated service manage transaction.
- Inject services, call trong transaction scope.
- Đảm bảo atomicity across services.

### QueryRunner / Prisma $transaction

- **QueryRunner**: TypeORM, manual control transaction.
- **Prisma $transaction**: Declarative, pass operations array.
- Chọn based on ORM.

Giữ transaction ở high level để consistency.