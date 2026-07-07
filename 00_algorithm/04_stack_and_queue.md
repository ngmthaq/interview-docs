# 4. What are stacks and queues? (Fresher)

Two fundamental linear structures differing in **access order**.

**Stack — LIFO** (Last In, First Out):

```ts
const stack: number[] = [];
stack.push(1); // add to top
stack.push(2);
stack.pop(); // 2 — removes the most recent
```

- Operations: `push`, `pop`, `peek` — all **O(1)**.
- Uses: **function call stack**, undo/redo, expression evaluation, DFS, backtracking, matching brackets.

**Queue — FIFO** (First In, First Out):

```ts
const queue: number[] = [];
queue.push(1); // enqueue at back
queue.push(2);
queue.shift(); // 1 — removes the oldest  (note: shift is O(n) on JS arrays)
```

- Operations: `enqueue`, `dequeue`, `peek` — **O(1)** with a proper implementation (linked list or two-pointer ring buffer).
- Uses: **BFS**, task scheduling, print/job queues, rate limiting.

**Variants:** **deque** (double-ended), **priority queue** (ordered by priority, usually a heap), **circular queue**.

**Key point:** a stack is LIFO (push/pop/peek, O(1)) powering call stacks, DFS, and undo; a queue is FIFO (enqueue/dequeue, O(1)) powering BFS and scheduling — pick by whether you need the newest or oldest element first.
