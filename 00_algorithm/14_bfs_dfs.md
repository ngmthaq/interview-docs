# 14. BFS vs DFS for graphs. (Mid)

Both traverse all reachable vertices in **O(V + E)**, differing in order and tooling.

**BFS — breadth-first, uses a queue** (explores level by level):

```ts
function bfs(graph: Record<string, string[]>, start: string): string[] {
  const visited = new Set([start]);
  const queue = [start];
  const order: string[] = [];
  while (queue.length) {
    const node = queue.shift()!;
    order.push(node);
    for (const next of graph[node]) {
      if (!visited.has(next)) {
        visited.add(next); // mark on enqueue to avoid duplicates
        queue.push(next);
      }
    }
  }
  return order;
}
```

**DFS — depth-first, uses a stack/recursion** (explores as deep as possible first):

```ts
function dfs(graph: Record<string, string[]>, node: string, visited = new Set<string>()) {
  visited.add(node);
  for (const next of graph[node]) {
    if (!visited.has(next)) dfs(graph, next, visited);
  }
  return visited;
}
```

**Choosing:**

- **BFS** — **shortest path in an unweighted graph**, level-order, nearest node.
- **DFS** — cycle detection, topological sort, connected components, path existence, backtracking.
- Always track a **`visited`** set to avoid infinite loops on cycles.

**Key point:** BFS (queue) explores level by level and finds shortest paths in unweighted graphs; DFS (stack/recursion) goes deep and powers cycle detection, topological sort, and components — both are O(V+E) and require a `visited` set to handle cycles.
