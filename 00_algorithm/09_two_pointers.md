# 9. What is the two-pointer technique? (Junior)

The **two-pointer** technique uses two indices moving through a data structure to solve problems in **O(n)** time and **O(1)** space — avoiding nested loops.

**Opposite ends** — e.g. pair-sum in a sorted array:

```ts
function twoSumSorted(arr: number[], target: number): [number, number] | null {
  let left = 0;
  let right = arr.length - 1;
  while (left < right) {
    const sum = arr[left] + arr[right];
    if (sum === target) return [left, right];
    if (sum < target)
      left++; // need a bigger sum
    else right--; // need a smaller sum
  }
  return null;
}
```

**Same direction (fast/slow)** — e.g. remove duplicates in place, or cycle detection:

```ts
// Slow builds the result, fast scans ahead
function removeDuplicates(arr: number[]): number {
  let slow = 0;
  for (let fast = 1; fast < arr.length; fast++) {
    if (arr[fast] !== arr[slow]) arr[++slow] = arr[fast];
  }
  return slow + 1; // new length
}
```

**Common uses:** pair/triplet sums (sorted), palindrome check, merging sorted arrays, removing duplicates, linked-list cycle detection (Floyd's).

**Key point:** two pointers — either converging from both ends or a fast/slow pair moving together — solve many array/list problems in O(n)/O(1), replacing nested loops; especially powerful on **sorted** data and for in-place modification.
