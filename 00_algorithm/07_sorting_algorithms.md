# 7. Compare common sorting algorithms. (Junior)

| Algorithm      | Average    | Worst      | Space    | Stable |
| -------------- | ---------- | ---------- | -------- | ------ |
| Bubble sort    | O(n²)      | O(n²)      | O(1)     | Yes    |
| Insertion sort | O(n²)      | O(n²)      | O(1)     | Yes    |
| Merge sort     | O(n log n) | O(n log n) | O(n)     | Yes    |
| Quick sort     | O(n log n) | O(n²)      | O(log n) | No     |
| Heap sort      | O(n log n) | O(n log n) | O(1)     | No     |

**Merge sort** — divide and conquer; split in half, sort each, merge:

```ts
function mergeSort(arr: number[]): number[] {
  if (arr.length <= 1) return arr;
  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));
  const result: number[] = [];
  let i = 0,
    j = 0;
  while (i < left.length && j < right.length) {
    result.push(left[i] <= right[j] ? left[i++] : right[j++]);
  }
  return [...result, ...left.slice(i), ...right.slice(j)];
}
```

**Picking one:**

- **Merge sort** — guaranteed O(n log n), **stable**, but O(n) extra space.
- **Quick sort** — fast in practice, in-place, but O(n²) worst case (mitigated by random/median pivots).
- **Heap sort** — O(n log n) worst case, O(1) space, not stable.
- **Stable** = equal elements keep their original order (matters when sorting by multiple keys).

**Key point:** comparison sorts bottom out at O(n log n) — merge sort is stable but uses O(n) space, quick sort is fast in-place but O(n²) worst case, heap sort guarantees O(n log n) in O(1) space; choose based on stability, memory, and worst-case needs.
