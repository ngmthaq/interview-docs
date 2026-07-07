# 18. Explain the MVC pattern. (Mid)

**MVC (Model-View-Controller)** is an architectural pattern that separates an application into three roles, improving maintainability and separation of concerns.

| Layer          | Responsibility                                         |
| -------------- | ------------------------------------------------------ |
| **Model**      | Data + business rules (the "what")                     |
| **View**       | Presentation / UI (the "how it looks")                 |
| **Controller** | Handles input, coordinates Model and View (the "glue") |

```ts
// Model
class UserModel {
  constructor(public name: string) {}
}

// View
class UserView {
  render(user: UserModel) {
    return `<h1>${user.name}</h1>`;
  }
}

// Controller
class UserController {
  constructor(private view: UserView) {}
  show(name: string) {
    const model = new UserModel(name); // build model
    return this.view.render(model); // hand to view
  }
}
```

**Benefits:**

- Each layer changes independently (swap the View without touching business logic).
- Parallel development and easier testing.

**Related:** MVVM (Vue/Angular), MVP — variations differing in how the view and logic communicate.
