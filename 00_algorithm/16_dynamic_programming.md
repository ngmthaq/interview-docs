# 16. What is dynamic programming? (Senior)

**Dynamic programming (DP)** solves problems by breaking them into **overlapping subproblems** and storing subproblem results to avoid recomputation. It applies when a problem has **optimal substructure** + **overlapping subproblems**.

**Two approaches:**

**Memoization (top-down)** — recursion + cache:

```ts
function fib(n: number, memo: Record<number, number> = {}): number {
  if (n <= 1) return n;
  if (memo[n] !== undefined) return memo[n]; // reuse
  return (memo[n] = fib(n - 1, memo) + fib(n - 2, memo));
}
```

**Tabulation (bottom-up)** — build a table iteratively:

```ts
function fibTab(n: number): number {
  if (n <= 1) return n;
  const dp = [0, 1];
  for (let i = 2; i <= n; i++) dp[i] = dp[i - 1] + dp[i - 2];
  return dp[n]; // (can optimize to O(1) space with two variables)
}
```

Naive `fib` is **O(2ⁿ)**; DP makes it **O(n)**.

**Recognizing DP problems:** "count the ways", "min/max cost", "longest/shortest" over choices — e.g. knapsack, coin change, edit distance, longest common subsequence, longest increasing subsequence.

**Key point:** DP trades space for time by caching results of overlapping subproblems (top-down memoization or bottom-up tabulation) when a problem has optimal substructure — turning exponential brute force into polynomial time for optimization and counting problems.
