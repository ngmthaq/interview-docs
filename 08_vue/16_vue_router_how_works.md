# Vue Router hoạt động thế nào?

- Dynamic route
- Navigation guard
- Protected route

## Chi tiết câu trả lời

Vue Router.

### Dynamic route

- Params: `/user/:id`
- useRoute() access params.

### Navigation guard

- beforeEach, beforeEnter.
- Check auth, redirect.

### Protected route

- Meta field cho auth.
- Guard check meta.

Router enable SPA navigation.
