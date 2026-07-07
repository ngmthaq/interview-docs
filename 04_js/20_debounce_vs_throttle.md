# 20. Debounce vs throttle? (Mid)

Both limit how often a function runs, but differently.

- **Debounce** — run only **after activity stops** for N ms. (e.g. search-as-you-type: wait until the user pauses.)
- **Throttle** — run **at most once every N ms** during continuous activity. (e.g. scroll/resize handlers.)

```js
function debounce(fn, delay) {
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => fn(...args), delay); // resets on each call
  };
}

function throttle(fn, limit) {
  let waiting = false;
  return (...args) => {
    if (waiting) return;
    fn(...args);
    waiting = true;
    setTimeout(() => (waiting = false), limit);
  };
}
```

```
Rapid events: | | | | | |     |
Debounce:                 X       (fires after the pause)
Throttle:     X    X    X    X    (fires on a fixed interval)
```

**Use cases:**

- **Debounce** → search input, autosave, resize-then-recompute.
- **Throttle** → scroll position, mouse move, rate-limiting API calls.

**Key point:** debounce waits for silence; throttle enforces a steady rate.
