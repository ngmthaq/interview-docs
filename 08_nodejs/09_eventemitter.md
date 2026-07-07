# 9. What is EventEmitter? (Junior)

**`EventEmitter`** is a core class implementing the **publish/subscribe** pattern — many Node APIs (streams, HTTP servers, sockets) are built on it.

```ts
import { EventEmitter } from "events";

class OrderService extends EventEmitter {
  placeOrder(id: string) {
    // ... save order ...
    this.emit("order:created", { id });
  }
}

const service = new OrderService();
service.on("order:created", ({ id }) => {
  console.log(`Send confirmation email for ${id}`);
});

service.placeOrder("A123"); // triggers the listener
```

**Key methods:**

- `on(event, listener)` — subscribe; `once(event, listener)` — fire only once.
- `emit(event, ...args)` — trigger all listeners synchronously.
- `off` / `removeListener` — unsubscribe (important to avoid leaks).

⚠️ Adding more than the default **10 listeners** logs a memory-leak warning; adjust with `setMaxListeners` if intentional. Always handle the special **`error`** event or it throws.

**Key point:** `EventEmitter` decouples producers from consumers via named events — it underpins streams and servers, and you extend it for your own event-driven logic.
