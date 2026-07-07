# 22. How does an ORM cause the N+1 problem, and how do you fix it? (Mid)

ORMs make N+1 easy to trigger through **lazy loading** — accessing a relation inside a loop fires one query per record.

```ts
// ❌ N+1: 1 query for users + 1 per user for their posts
const users = await userRepo.find();
for (const u of users) {
  console.log(u.posts.length); // lazy-loads posts → a query each iteration
}
```

**Fix — eager load the relation in one shot:**

```ts
// TypeORM
const users = await userRepo.find({ relations: { posts: true } });

// Prisma
const users = await prisma.user.findMany({ include: { posts: true } });

// Sequelize
const users = await User.findAll({ include: [Post] });
```

Now the ORM emits a single JOIN (or a batched `WHERE IN`) instead of N queries.

**Key point:** know your ORM's **eager vs lazy** loading. Enable query logging in dev to _see_ how many queries a request actually makes — the surest way to catch N+1. See [09_n_plus_1_problem].
