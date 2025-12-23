# Deploy xong production bị lỗi nghiêm trọng

- Rollback
- Feature flag
- Canary / blue-green deploy

## Chi tiết câu trả lời

Khi deploy production lỗi:

### 1. Rollback

- Quick rollback to previous version.
- Have rollback scripts ready.
- Ưu điểm: Fast recovery.

### 2. Feature Flag

- Disable problematic feature via flag.
- Ưu điểm: Selective rollback.

### 3. Canary / Blue-Green Deploy

- Deploy to subset of users (canary).
- Full switch only if successful (blue-green).
- Ưu điểm: Minimize impact, easy rollback.

Implement monitoring, automated tests pre-deploy.
