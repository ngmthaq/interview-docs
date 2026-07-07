# 28. Promise.all vs allSettled vs race vs any. (Mid)

The four **Promise combinators** coordinate multiple promises differently.

```js
const p1 = fetch("/a");
const p2 = fetch("/b");
```

**`Promise.all`** — waits for **all**; rejects if **any** rejects (fail-fast):

```js
const [a, b] = await Promise.all([p1, p2]); // both resolved, or throws
```

**`Promise.allSettled`** — waits for all; **never rejects**, returns each outcome:

```js
const results = await Promise.allSettled([p1, p2]);
// [{ status: "fulfilled", value }, { status: "rejected", reason }]
```

**`Promise.race`** — settles with the **first** to settle (fulfill **or** reject):

```js
await Promise.race([fetch("/x"), timeout(5000)]); // useful for timeouts
```

**`Promise.any`** — resolves with the **first fulfilled**; rejects only if **all** reject (`AggregateError`):

```js
await Promise.any([mirror1, mirror2, mirror3]); // first success wins
```

|              | Resolves when  | Rejects when              |
| ------------ | -------------- | ------------------------- |
| `all`        | all fulfill    | any rejects               |
| `allSettled` | all settle     | never                     |
| `race`       | first settles  | first settles (if reject) |
| `any`        | first fulfills | all reject                |

**Key point:** `all` (all-or-nothing, fail-fast), `allSettled` (collect every outcome), `race` (first to settle — good for timeouts), `any` (first success) — pick the combinator matching whether you need all results, all outcomes, or the fastest/first winner.
