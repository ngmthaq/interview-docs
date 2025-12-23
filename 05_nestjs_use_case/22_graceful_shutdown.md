# Graceful shutdown trong NestJS

- `app.enableShutdownHooks()`
- `process.on('SIGTERM')`
- Đóng DB, queue, worker

## Chi tiết câu trả lời

Graceful shutdown.

### app.enableShutdownHooks()

- Enable hooks cho onModuleDestroy.
- Cleanup resources khi shutdown.

### process.on('SIGTERM')

- Listen SIGTERM signal.
- Perform cleanup before exit.

### Đóng DB, queue, worker

- Close DB connections.
- Drain queues.
- Wait workers finish.
- Timeout để force exit.

Ensure no data loss, clean shutdown.