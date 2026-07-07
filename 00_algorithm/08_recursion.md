# 8. What is recursion? (Junior)

**Recursion** is when a function calls itself to solve smaller instances of a problem, until reaching a **base case** that stops the recursion.

```ts
function factorial(n: number): number {
  if (n <= 1) return 1; // base case — stops recursion
  return n * factorial(n - 1); // recursive case — smaller subproblem
}
factorial(5); // 5 * 4 * 3 * 2 * 1 = 120
```

**Every recursive function needs:**

1. **Base case(s)** — condition(s) that return without recursing (prevents infinite recursion).
2. **Recursive case** — calls itself with input moving **toward** the base case.

**Cost:**

- Each call adds a frame to the **call stack** → **O(depth) space**.
- Too-deep recursion causes a **stack overflow** — convert to iteration or use tail-call/explicit stack for very deep cases.

**Recursion vs iteration:** recursion is cleaner for **tree/graph traversal**, divide-and-conquer, and backtracking; iteration avoids stack overhead. Any recursion can be rewritten iteratively (often with an explicit stack).

**Key point:** recursion solves a problem via smaller self-calls with a base case to terminate; it's elegant for trees, divide-and-conquer, and backtracking but consumes O(depth) stack space and risks stack overflow — trade off against iteration accordingly.
