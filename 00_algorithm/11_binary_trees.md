# 11. What is a binary tree and a BST? (Mid)

A **binary tree** is a hierarchy where each node has at most **two children** (left, right). A **Binary Search Tree (BST)** adds an ordering invariant: for every node, **left subtree < node < right subtree**.

```ts
class TreeNode {
  value: number;
  left: TreeNode | null = null;
  right: TreeNode | null = null;
  constructor(value: number) {
    this.value = value;
  }
}
```

**BST operations** (average **O(log n)** when balanced):

```ts
function search(root: TreeNode | null, target: number): TreeNode | null {
  if (!root || root.value === target) return root;
  return target < root.value
    ? search(root.left, target) // go left
    : search(root.right, target); // go right
}
```

**Key facts:**

- **Balanced** BST → O(log n) search/insert/delete; **degenerate** (sorted inserts) → O(n) like a linked list.
- **In-order traversal** of a BST yields values in **sorted order**.
- **Self-balancing** variants (AVL, Red-Black) guarantee O(log n) by rebalancing on insert/delete.

**Terms:** height, depth, leaf, complete/full/perfect tree, balanced.

**Key point:** a binary tree caps children at two; a BST keeps left < node < right for O(log n) search/insert/delete when balanced (degrading to O(n) if skewed) — in-order traversal gives sorted output, and AVL/Red-Black trees stay balanced automatically.
