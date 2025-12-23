# Migration DB trong production thế nào cho an toàn?

- Backward compatible schema
- Deploy code trước
- Migrate sau

## Chi tiết câu trả lời

DB migration an toàn:

### 1. Backward Compatible Schema

- Design migrations không break existing code.
- Add columns nullable, don't remove immediately.
- Ưu điểm: Zero-downtime.

### 2. Deploy Code Trước

- Deploy app code supporting both old/new schema.
- Then run migration.
- Ưu điểm: App handles both versions.

### 3. Migrate Sau

- Run migration in small batches nếu large data.
- Monitor performance impact.
- Have rollback plan.

Use tools như Flyway, Liquibase. Test thoroughly.
