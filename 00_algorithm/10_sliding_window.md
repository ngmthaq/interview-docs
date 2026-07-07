# 10. What is the sliding window technique? (Mid)

The **sliding window** maintains a contiguous range (subarray/substring) that **expands and contracts** as it moves through the data — turning many O(n²) subarray problems into **O(n)**.

**Fixed-size window** — e.g. max sum of k consecutive elements:

```ts
function maxSubarraySum(arr: number[], k: number): number {
  let windowSum = 0;
  for (let i = 0; i < k; i++) windowSum += arr[i]; // first window
  let max = windowSum;
  for (let i = k; i < arr.length; i++) {
    windowSum += arr[i] - arr[i - k]; // slide: add new, drop old
    max = Math.max(max, windowSum);
  }
  return max;
}
```

**Variable-size window** — e.g. longest substring without repeating characters:

```ts
function longestUnique(s: string): number {
  const seen = new Set<string>();
  let left = 0,
    best = 0;
  for (let right = 0; right < s.length; right++) {
    while (seen.has(s[right])) seen.delete(s[left++]); // shrink until valid
    seen.add(s[right]);
    best = Math.max(best, right - left + 1);
  }
  return best;
}
```

**Recognize it when:** a problem asks for the best/longest/shortest **contiguous** subarray or substring meeting a condition.

**Key point:** the sliding window reuses work by adding one element and removing another as it moves, solving contiguous subarray/substring problems in O(n); use a fixed window for size-k problems and a variable window (expand/shrink) for condition-based ones.
