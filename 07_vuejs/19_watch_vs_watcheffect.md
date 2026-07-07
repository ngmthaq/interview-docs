# 19. `watch` vs `watchEffect`? (Mid)

Both run side effects on reactive changes; they differ in **how dependencies are tracked**.

**`watch`** — **explicit** source(s). Lazy by default; gives old + new values:

```ts
watch(query, (newVal, oldVal) => {
  fetchResults(newVal);
});
```

**`watchEffect`** — **automatic** dependency tracking. Runs immediately and re-runs when any reactive value **used inside** changes:

```ts
watchEffect(() => {
  console.log(`query is ${query.value}, page ${page.value}`);
  // tracks query and page automatically
});
```

|               | `watch`                    | `watchEffect`               |
| ------------- | -------------------------- | --------------------------- |
| Dependencies  | explicit source            | auto-collected from body    |
| Runs on setup | lazy (unless `immediate`)  | immediately                 |
| Old value     | ✅ available               | ❌ not available            |
| Best for      | specific source → reaction | multiple deps, sync effects |

**When to use each:**

- **`watch`** — you know exactly what to watch, need the previous value, or want lazy execution (e.g. react to a specific id change).
- **`watchEffect`** — the effect naturally depends on several reactive values and you want them tracked automatically.

**Cleanup** — both support `onCleanup` for canceling stale work:

```ts
watchEffect((onCleanup) => {
  const ctrl = new AbortController();
  fetch(url.value, { signal: ctrl.signal });
  onCleanup(() => ctrl.abort());
});
```

**Gotcha:** `watchEffect` only tracks deps that are **actually accessed** on a run — a value behind a false `if` branch won't be tracked until reached.
