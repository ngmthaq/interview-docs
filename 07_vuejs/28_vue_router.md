# 28. Vue Router basics? (Mid)

Vue Router is the official client-side router for SPAs — it maps URLs to components without full-page reloads.

**Setup:**

```ts
import { createRouter, createWebHistory } from "vue-router";

const router = createRouter({
  history: createWebHistory(),
  routes: [
    { path: "/", component: Home },
    { path: "/users/:id", component: User }, // dynamic segment
    { path: "/:pathMatch(.*)*", component: NotFound }, // 404
  ],
});
app.use(router);
```

**Render + navigate** in templates:

```vue
<router-link to="/users/1">User 1</router-link>
<router-view />
<!-- matched component renders here -->
```

**Programmatic navigation & route data** via composables:

```ts
import { useRouter, useRoute } from "vue-router";
const router = useRouter();
const route = useRoute();

router.push("/users/2"); // navigate
router.push({ name: "user", params: { id: 2 } });
const id = route.params.id; // read params
const q = route.query.search; // read query string
```

**Key features:**

- **Dynamic routes** — `/users/:id`, read via `route.params`.
- **Nested routes** — `children` + nested `<router-view>`.
- **Named routes** — navigate by `name` instead of hardcoded paths.
- **Lazy loading** — `component: () => import('./Page.vue')` for code splitting.

**Navigation guards** — run logic before navigation (auth, confirmation):

```ts
router.beforeEach((to, from) => {
  if (to.meta.requiresAuth && !isLoggedIn()) return "/login";
});
```

**History modes:** `createWebHistory` (clean URLs, needs server config) vs `createWebHashHistory` (`#`-based, no server config).
