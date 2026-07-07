# 17. What are greedy algorithms? (Senior)

A **greedy algorithm** makes the **locally optimal choice at each step**, hoping it leads to a global optimum. It's simpler and faster than DP but only correct for problems with the **greedy-choice property**.

```ts
// Coin change (greedy) — works for "canonical" coin systems like [25,10,5,1]
function coinChangeGreedy(coins: number[], amount: number): number {
  coins.sort((a, b) => b - a); // largest first
  let count = 0;
  for (const coin of coins) {
    while (amount >= coin) {
      amount -= coin; // take as many of the biggest coin as possible
      count++;
    }
  }
  return amount === 0 ? count : -1;
}
```

**When greedy works — it needs:**

- **Greedy-choice property** — a local optimum leads to a global optimum.
- **Optimal substructure** — the optimal solution contains optimal sub-solutions.

**Classic greedy problems:** activity/interval scheduling, Huffman coding, Dijkstra's & Prim's/Kruskal's (MST), fractional knapsack.

**Greedy vs DP:** greedy commits to a choice and never reconsiders (faster, O(n log n)-ish); DP explores all choices (slower but always correct when applicable). **Warning:** greedy coin change **fails** for arbitrary denominations (e.g. `[1,3,4]`, amount 6) — DP is needed there.

**Key point:** greedy algorithms take the best local choice each step and never backtrack — fast and simple, but only correct when the problem has the greedy-choice property (scheduling, Huffman, Dijkstra, MST); otherwise use DP, since greedy can miss the global optimum.
