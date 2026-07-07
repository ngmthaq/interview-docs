# 16. Explain map, filter, and reduce. (Junior)

Three core array methods for transforming data **without mutating** the original.

```js
const nums = [1, 2, 3, 4];

// map — transform each element → new array of same length
nums.map((n) => n * 2); // [2, 4, 6, 8]

// filter — keep elements that pass a test → shorter array
nums.filter((n) => n % 2 === 0); // [2, 4]

// reduce — collapse to a single value
nums.reduce((acc, n) => acc + n, 0); // 10
```

| Method   | Returns                | Use for                             |
| -------- | ---------------------- | ----------------------------------- |
| `map`    | New array, same length | Transforming each item              |
| `filter` | New array, ≤ length    | Selecting items                     |
| `reduce` | Any single value       | Summing, grouping, building objects |

**Chaining:**

```js
const total = orders
  .filter((o) => o.paid)
  .map((o) => o.amount)
  .reduce((sum, a) => sum + a, 0);
```

**reduce building an object:**

```js
["a", "b", "a"].reduce((acc, k) => {
  acc[k] = (acc[k] || 0) + 1;
  return acc;
}, {}); // { a: 2, b: 1 }
```

**Key point:** these are **pure**, non-mutating, and composable — cleaner than manual `for` loops for data transformation.
