# 20. How do you choose the right data structure? (Senior)

Picking the right structure is often the difference between an O(n²) and an O(n) solution. Match the structure to the **operations you perform most**.

**Decision guide by need:**

- **Fast lookup / dedup / counting by key** → **Hash map / Set** (O(1) avg).
- **Ordered data + range queries / sorted iteration** → **Balanced BST / sorted array** (O(log n)).
- **Always need the min/max / top-K / priority** → **Heap** (O(log n) insert/extract).
- **LIFO (undo, DFS, matching)** → **Stack**.
- **FIFO (scheduling, BFS)** → **Queue / deque**.
- **Frequent front/middle insert-delete** → **Linked list**.
- **Random access / iteration / cache locality** → **Array**.
- **Prefix/autocomplete on strings** → **Trie**.
- **Connectivity / grouping (union-find)** → **Disjoint Set (DSU)**.

**Questions to ask:**

1. What operations dominate (search, insert, delete, min/max, order)?
2. What are the **frequency** and required **complexity** of each?
3. Is **ordering** needed? Are **keys** unique?
4. What are the **memory** constraints?

```ts
// Example: "first non-repeating char" → hash map for counts (O(n)) beats nested loops (O(n²))
```

**Key point:** choose a data structure by the operations you do most — hash maps for O(1) lookups, heaps for priorities/top-K, BSTs for ordered range queries, stacks/queues for LIFO/FIFO, tries for prefixes, union-find for connectivity — the right choice often collapses a brute-force O(n²) into O(n) or O(n log n).
