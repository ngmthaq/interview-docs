# 24. How does NestJS support microservices? (Senior)

Nest has a dedicated **microservices** layer (`@nestjs/microservices`) that swaps HTTP for a **transport** (TCP, Redis, NATS, RabbitMQ, Kafka, gRPC) while keeping the same controller/provider model.

```ts
// bootstrap a microservice
const app = await NestFactory.createMicroservice(AppModule, {
  transport: Transport.TCP,
  options: { host: "0.0.0.0", port: 3001 },
});
await app.listen();
```

**Message patterns** — request/response vs event:

```ts
@MessagePattern({ cmd: "get_user" }) // responds to a request
getUser(@Payload() id: string) {
  return this.usersService.findOne(id);
}

@EventPattern("user_created") // fire-and-forget event
handleUserCreated(@Payload() data: UserCreatedEvent) {
  this.emailService.sendWelcome(data);
}
```

Clients send via a `ClientProxy` (`client.send(...)` for request/response, `client.emit(...)` for events).

**Key point:** Nest microservices reuse the familiar controller/DI model over pluggable transports (TCP/Redis/NATS/Kafka/gRPC); `@MessagePattern` handles request/response and `@EventPattern` handles fire-and-forget events, decoupling services via messaging.
