# E2E test khác gì integration test trong NestJS?

- Supertest
- Test module vs app thật
- Khi nào chạy E2E

## Chi tiết câu trả lời

Difference between E2E and integration tests.

### Supertest

- HTTP testing library.
- Test API endpoints.
- Simulate real requests.

### Test module vs app thật

- **Integration**: Test modules với real DB, mocks external.
- **E2E**: Test full app, real DB, external services.
- Integration faster, E2E comprehensive.

### Khi nào chạy E2E

- Critical user flows.
- After major changes.
- CI/CD pipeline.
- Not for every commit (slow).

Balance với integration tests.