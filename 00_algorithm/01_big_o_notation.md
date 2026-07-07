# 1. What is Big O notation? (Fresher)

**Big O** describes how an algorithm's **time or space** grows relative to input size **n** — the worst-case upper bound, ignoring constants and lower-order terms.

**Common complexities (best → worst):**

| Big O      | Name         | Example                            |
| ---------- | ------------ | ---------------------------------- |
| O(1)       | Constant     | Array index access, hash lookup    |
| O(log n)   | Logarithmic  | Binary search                      |
| O(n)       | Linear       | Single loop over an array          |
| O(n log n) | Linearithmic | Efficient sorts (merge, quick avg) |
| O(n²)      | Quadratic    | Nested loops (bubble sort)         |
| O(2ⁿ)      | Exponential  | Naive recursive Fibonacci          |

```ts
// O(1) — one operation regardless of size
const first = (arr: number[]) => arr[0];

// O(n) — grows linearly
const sum = (arr: number[]) => arr.reduce((a, b) => a + b, 0);

// O(n²) — nested loop
function hasDuplicate(arr: number[]): boolean {
  for (let i = 0; i < arr.length; i++)
    for (let j = i + 1; j < arr.length; j++) if (arr[i] === arr[j]) return true;
  return false;
}
```

**Rules:** drop constants (O(2n) → O(n)) and non-dominant terms (O(n² + n) → O(n²)).

**Key point:** Big O expresses growth rate as input scales, ignoring constants/lower-order terms — it's the vocabulary for comparing algorithm efficiency, from O(1) constant to O(2ⁿ) exponential.
