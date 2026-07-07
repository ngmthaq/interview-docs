# 15. Recursion vs iteration — trade-offs. (Mid)

Both repeat work; they differ in mechanism, cost, and readability.

```ts
// Recursive — elegant, but O(n) call-stack space
function sumR(n: number): number {
  return n === 0 ? 0 : n + sumR(n - 1);
}

// Iterative — O(1) space, no stack risk
function sumI(n: number): number {
  let total = 0;
  for (let i = 1; i <= n; i++) total += i;
  return total;
}
```

|             | Recursion                        | Iteration                |
| ----------- | -------------------------------- | ------------------------ |
| Space       | O(depth) call stack              | O(1) (usually)           |
| Readability | Cleaner for trees/divide-conquer | Cleaner for linear loops |
| Risk        | Stack overflow if too deep       | None                     |
| Speed       | Function-call overhead           | Slightly faster          |

**Key points:**

- Any recursion can be rewritten **iteratively**, sometimes with an **explicit stack** (to mimic the call stack) for tree/graph traversal.
- **Tail recursion** (recursive call is the last operation) can be optimized to O(1) space in some languages — but **JS engines generally don't** do tail-call optimization, so deep recursion still overflows.
- Prefer recursion for naturally recursive structures (trees, backtracking); prefer iteration for simple linear processing or when depth is large.

**Key point:** recursion is cleaner for recursive structures but costs O(depth) stack space and risks overflow (JS lacks reliable tail-call optimization); iteration uses O(1) space and is safer for deep/linear work — convert deep recursion to iteration with an explicit stack when needed.
