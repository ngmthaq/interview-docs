# 13. Explain the Observer pattern. (Mid)

**Observer** defines a **one-to-many** dependency: when one object (**subject**) changes state, all its **observers** are notified automatically. The backbone of event-driven systems.

```ts
type Observer = (data: string) => void;

class Subject {
  private observers: Observer[] = [];

  subscribe(fn: Observer) {
    this.observers.push(fn);
  }
  unsubscribe(fn: Observer) {
    this.observers = this.observers.filter((o) => o !== fn);
  }
  notify(data: string) {
    this.observers.forEach((o) => o(data));
  }
}

const news = new Subject();
news.subscribe((msg) => console.log("User A got:", msg));
news.notify("Breaking!"); // all subscribers notified
```

**Benefits:**

- Loose coupling — subject doesn't know concrete observers.
- Dynamic subscribe/unsubscribe at runtime.

Real-world: DOM events, RxJS, Redux/Vuex store subscriptions, pub/sub messaging.
