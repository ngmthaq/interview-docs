# Cron job / background task trong NestJS

- `@nestjs/schedule`
- Queue (Bull / BullMQ)
- Khi nào không nên dùng cron trong app chính

## Chi tiết câu trả lời

Background tasks trong NestJS.

### @nestjs/schedule

- Built-in cron decorators (@Cron, @Interval).
- Simple cho recurring tasks.
- Run trong app process.

### Queue (Bull / BullMQ)

- Asynchronous job processing.
- Durable, scalable.
- Separate workers.

### Khi nào không nên dùng cron trong app chính

- High load tasks: Affect app performance.
- Long-running: Block app startup/shutdown.
- Critical tasks: Need monitoring, retry.

Use separate service cho heavy background work.