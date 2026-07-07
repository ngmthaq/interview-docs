# 12. What are the tree traversal methods? (Mid)

Two families: **depth-first (DFS)** and **breadth-first (BFS)**.

**DFS — three orders** (differ by when the node is visited):

```ts
function inorder(node: TreeNode | null, out: number[] = []): number[] {
  if (!node) return out;
  inorder(node.left, out); // left
  out.push(node.value); // node   (in-order: L → N → R)
  inorder(node.right, out); // right
  return out;
}
```

- **In-order (L, N, R)** — sorted output for a BST.
- **Pre-order (N, L, R)** — copy/serialize a tree.
- **Post-order (L, R, N)** — delete a tree, evaluate expressions (children before parent).

**BFS — level-order** using a queue:

```ts
function levelOrder(root: TreeNode | null): number[] {
  const out: number[] = [];
  const queue = root ? [root] : [];
  while (queue.length) {
    const node = queue.shift()!;
    out.push(node.value);
    if (node.left) queue.push(node.left);
    if (node.right) queue.push(node.right);
  }
  return out;
}
```

**Choosing:** BFS finds the **shortest path**/nearest level; DFS explores deep (path-finding, subtree computations). Both are **O(n)** time; DFS uses O(height) stack, BFS uses O(width) queue.

**Key point:** DFS visits deep first in pre/in/post order (in-order = sorted BST, post-order = children-first), while BFS/level-order uses a queue to visit level by level; both are O(n), and BFS is the tool for shortest-path/nearest-level questions.
