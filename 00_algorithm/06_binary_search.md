# 6. Explain binary search. (Junior)

**Binary search** finds a target in a **sorted** array in **O(log n)** by repeatedly halving the search range.

```ts
function binarySearch(arr: number[], target: number): number {
  let low = 0;
  let high = arr.length - 1;

  while (low <= high) {
    const mid = Math.floor((low + high) / 2); // or low + (high-low)/2 to avoid overflow
    if (arr[mid] === target) return mid;
    if (arr[mid] < target)
      low = mid + 1; // search right half
    else high = mid - 1; // search left half
  }
  return -1; // not found
}
```

**How it works:** compare the middle element; if it's the target, done. If the target is larger, discard the left half; if smaller, discard the right half. Each step halves the candidates → **log₂ n** steps.

**Requirements & pitfalls:**

- The array **must be sorted**.
- Use `low + (high - low) / 2` to avoid integer overflow in other languages.
- Watch the boundary conditions (`<=` vs `<`, `mid ± 1`) — off-by-one errors are common.

**Variants:** find first/last occurrence, find insertion point (lower/upper bound), search in a rotated array, or binary-search over an answer space.

**Key point:** binary search halves a **sorted** range each step for O(log n) lookup; it requires sorted data and careful boundary handling, and generalizes to finding insertion points, first/last occurrences, and "search the answer space" problems.
