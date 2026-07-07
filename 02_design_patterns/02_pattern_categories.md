# 2. What are the three categories of design patterns? (Fresher)

The GoF patterns split into three groups by **what problem they solve**.

| Category       | Concern                                             | Examples                                     |
| -------------- | --------------------------------------------------- | -------------------------------------------- |
| **Creational** | How objects are **created**                         | Singleton, Factory, Builder, Prototype       |
| **Structural** | How objects are **composed** into bigger structures | Adapter, Decorator, Facade, Proxy, Composite |
| **Behavioral** | How objects **communicate & share responsibility**  | Observer, Strategy, Command, State           |

```ts
// Creational: control construction
const user = UserFactory.create("admin");

// Structural: wrap/compose
const service = new CachingProxy(new ApiService());

// Behavioral: define interaction
button.addEventListener("click", handler); // Observer-like
```

**Interview tip:** if you can slot a named pattern into the right category and say _why_, you show real understanding rather than memorization.
