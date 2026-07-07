# 12. Explain the Composite pattern. (Mid)

**Composite** lets you treat **individual objects and groups of objects uniformly** through a common interface — modeling **tree structures** (part-whole hierarchies).

```ts
interface FileSystemNode {
  size(): number;
}

class FileLeaf implements FileSystemNode {
  constructor(private bytes: number) {}
  size() {
    return this.bytes;
  }
}

class Folder implements FileSystemNode {
  private children: FileSystemNode[] = [];
  add(node: FileSystemNode) {
    this.children.push(node);
  }
  size() {
    return this.children.reduce((sum, c) => sum + c.size(), 0);
  }
}

const root = new Folder();
root.add(new FileLeaf(100));
const sub = new Folder();
sub.add(new FileLeaf(50));
root.add(sub);
root.size(); // 150 — works recursively
```

**Key point:** the client calls `size()` without caring whether it's a single file or a whole folder tree. Great for file systems, UI component trees, org charts, menus.
