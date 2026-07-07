# 13. How do you represent a graph? (Mid)

A **graph** is a set of **vertices (nodes)** connected by **edges**. Graphs can be **directed/undirected** and **weighted/unweighted**.

**Two main representations:**

**Adjacency list** — each vertex maps to its neighbors (space O(V + E)):

```ts
const graph: Record<string, string[]> = {
  A: ["B", "C"],
  B: ["A", "D"],
  C: ["A", "D"],
  D: ["B", "C"],
};
// weighted: Map<string, { node: string; weight: number }[]>
```

**Adjacency matrix** — a V×V grid where `matrix[i][j]` marks an edge (space O(V²)):

```ts
// A=0, B=1, C=2, D=3
const matrix = [
  [0, 1, 1, 0],
  [1, 0, 0, 1],
  [1, 0, 0, 1],
  [0, 1, 1, 0],
];
```

|             | Adjacency list | Adjacency matrix |
| ----------- | -------------- | ---------------- |
| Space       | O(V + E)       | O(V²)            |
| Edge lookup | O(degree)      | O(1)             |
| Best for    | Sparse graphs  | Dense graphs     |

**Key point:** graphs are vertices + edges (directed/weighted variants); an adjacency list (O(V+E)) suits sparse graphs and iterating neighbors, while an adjacency matrix (O(V²)) gives O(1) edge lookups and suits dense graphs — the list is the common default.
