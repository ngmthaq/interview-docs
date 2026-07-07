# 34. What is useSyncExternalStore? (Senior)

**`useSyncExternalStore`** subscribes a component to an **external store** (state living outside React) in a way that's **safe for concurrent rendering** and SSR. It's the hook state-management libraries (Redux, Zustand) use internally.

```tsx
import { useSyncExternalStore } from "react";

// A tiny external store
function createStore(initial) {
  let state = initial;
  const listeners = new Set<() => void>();
  return {
    getSnapshot: () => state,
    subscribe: (cb) => (listeners.add(cb), () => listeners.delete(cb)),
    set: (next) => {
      state = next;
      listeners.forEach((l) => l());
    },
  };
}

const store = createStore(0);

function Counter() {
  const count = useSyncExternalStore(store.subscribe, store.getSnapshot);
  return <button onClick={() => store.set(count + 1)}>{count}</button>;
}
```

**Three arguments:**

1. **`subscribe(callback)`** — register for store changes; returns an unsubscribe fn.
2. **`getSnapshot()`** — return the current value (must be referentially stable when unchanged).
3. **`getServerSnapshot()`** _(optional)_ — value for SSR/hydration.

**Why it exists:** it prevents **tearing** (different components seeing different store values) during concurrent rendering — something naive `useState`+subscription patterns can't guarantee.

**Key point:** `useSyncExternalStore(subscribe, getSnapshot, getServerSnapshot?)` safely binds components to external/non-React state, avoiding tearing under concurrent rendering and supporting SSR — the official primitive powering external state libraries.
