# React là gì? Vấn đề React giải quyết?

- UI = function của state
- Component-based
- Virtual DOM giải quyết gì?

## Chi tiết câu trả lời

React là thư viện JavaScript để xây dựng giao diện người dùng.

### UI = function của state

- Giao diện là hàm của trạng thái (state).
- Khi state thay đổi, UI tự động cập nhật.
- Declarative programming: Mô tả UI ở trạng thái nào, React xử lý render.

### Component-based

- Chia UI thành components tái sử dụng.
- Mỗi component quản lý state và logic riêng.
- Dễ maintain, test, và scale.

### Virtual DOM giải quyết gì?

- Virtual DOM là representation ảo của DOM thật.
- React so sánh (diff) Virtual DOM trước/sau để tìm thay đổi tối thiểu.
- Giảm thao tác DOM trực tiếp, cải thiện performance.
- Reconciliation algorithm tối ưu updates.

React giải quyết vấn đề UI phức tạp, state management, và performance trong web apps.
