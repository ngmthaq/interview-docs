# 10. Explain the Facade pattern. (Junior → Mid)

**Facade** provides a **simple, unified interface** over a complex subsystem, hiding its internals from the client.

```ts
class Cpu {
  freeze() {}
  jump(pos: number) {}
  execute() {}
}
class Memory {
  load(pos: number, data: string) {}
}
class Disk {
  read(): string {
    return "boot data";
  }
}

// Facade wraps the messy startup sequence
class ComputerFacade {
  private cpu = new Cpu();
  private memory = new Memory();
  private disk = new Disk();

  start() {
    this.cpu.freeze();
    this.memory.load(0, this.disk.read());
    this.cpu.jump(0);
    this.cpu.execute();
  }
}

new ComputerFacade().start(); // client just calls start()
```

**Benefits:**

- Reduces coupling — clients depend on the facade, not many subsystems.
- Simpler API for common use cases (the subsystem is still there for advanced needs).

**Adapter vs Facade:** Adapter _changes_ an interface to match; Facade _simplifies_ a set of interfaces into one.
