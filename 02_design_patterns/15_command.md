# 15. Explain the Command pattern. (Mid)

**Command** turns a **request into a standalone object**, containing everything needed to perform an action. This lets you queue, log, undo, or parameterize operations.

```ts
interface Command {
  execute(): void;
  undo(): void;
}

class AddTextCommand implements Command {
  constructor(
    private doc: string[],
    private text: string,
  ) {}
  execute() {
    this.doc.push(this.text);
  }
  undo() {
    this.doc.pop();
  }
}

class Invoker {
  private history: Command[] = [];
  run(cmd: Command) {
    cmd.execute();
    this.history.push(cmd);
  }
  undoLast() {
    this.history.pop()?.undo();
  }
}

const doc: string[] = [];
const invoker = new Invoker();
invoker.run(new AddTextCommand(doc, "Hello"));
invoker.undoLast(); // reverts
```

**Benefits:**

- Enables **undo/redo**, command **queues**, and **logging/replay**.
- Decouples the object that _invokes_ an action from the one that _performs_ it.

Real-world: editor undo stacks, task queues, transactional operations.
