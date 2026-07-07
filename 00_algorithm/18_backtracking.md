# 18. What is backtracking? (Senior)

**Backtracking** builds a solution incrementally and **abandons ("backtracks") a path** as soon as it violates constraints — a systematic, pruned brute-force over all candidates.

```ts
// Generate all permutations of an array
function permute(nums: number[]): number[][] {
  const result: number[][] = [];

  function backtrack(current: number[], remaining: number[]) {
    if (remaining.length === 0) {
      result.push([...current]); // complete solution
      return;
    }
    for (let i = 0; i < remaining.length; i++) {
      current.push(remaining[i]); // choose
      backtrack(current, [...remaining.slice(0, i), ...remaining.slice(i + 1)]); // explore
      current.pop(); // un-choose (backtrack)
    }
  }

  backtrack([], nums);
  return result;
}
```

**The pattern: choose → explore → un-choose.** Prune branches that can't lead to a valid solution to cut the search space.

**Classic backtracking problems:** permutations/combinations/subsets, N-Queens, Sudoku solver, word search, generating parentheses, graph coloring, maze/path finding.

**Complexity:** often exponential (e.g. O(n!) for permutations) — pruning and constraint checks make it feasible in practice.

**Key point:** backtracking explores candidates via choose → explore → un-choose, pruning invalid partial solutions early — the go-to approach for permutations/combinations, constraint puzzles (N-Queens, Sudoku), and path-finding; inherently exponential but tamed by aggressive pruning.
