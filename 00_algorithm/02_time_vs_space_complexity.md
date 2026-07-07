# 2. Time vs space complexity. (Fresher)

Both use Big O, but measure different resources:

- **Time complexity** — how the **number of operations** grows with input size.
- **Space complexity** — how much **extra memory** an algorithm uses relative to input size (excluding the input itself).

```ts
// Time: O(n) — one pass.  Space: O(n) — the Set can hold n items.
function unique(arr: number[]): number[] {
  const seen = new Set<number>();
  const result: number[] = [];
  for (const x of arr) {
    if (!seen.has(x)) {
      seen.add(x);
      result.push(x);
    }
  }
  return result;
}

// Time: O(n).  Space: O(1) — only a couple of variables.
function sum(arr: number[]): number {
  let total = 0;
  for (const x of arr) total += x;
  return total;
}
```

**The trade-off:** you can often **trade space for time** — e.g. a hash map (extra memory) turns an O(n²) nested search into O(n). Recursion adds **O(depth)** space from the call stack.

**Key point:** time complexity counts operations, space complexity counts extra memory; they often trade off — using more memory (hash maps, caching) can reduce time — and recursion consumes stack space proportional to its depth.
