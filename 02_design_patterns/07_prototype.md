# 7. Explain the Prototype pattern. (Mid)

**Prototype** creates new objects by **cloning an existing instance** instead of constructing from scratch. Useful when construction is expensive or you want a preconfigured copy.

```ts
interface Cloneable<T> {
  clone(): T;
}

class Document implements Cloneable<Document> {
  constructor(
    public title: string,
    public config: Record<string, unknown>,
  ) {}

  clone(): Document {
    // deep copy so the clone doesn't share references
    return new Document(this.title, structuredClone(this.config));
  }
}

const template = new Document("Invoice", { currency: "USD" });
const copy = template.clone();
```

**When to use:**

- Building many similar objects from a costly-to-create template.
- Avoiding subclass explosion just to vary initial state.

**Watch out:** decide between **shallow vs deep copy** — a shallow clone shares nested references, which can cause subtle bugs.
