# 25. How do you build a GraphQL API in NestJS? (Senior)

Nest's `@nestjs/graphql` (over Apollo/Mercurius) supports a **code-first** approach: you write TypeScript classes and Nest generates the schema.

```ts
// object type
@ObjectType()
export class Author {
  @Field(() => Int) id: number;
  @Field() name: string;
  @Field(() => [Post]) posts: Post[];
}

// resolver — the GraphQL equivalent of a controller
@Resolver(() => Author)
export class AuthorsResolver {
  constructor(private authorsService: AuthorsService) {}

  @Query(() => Author)
  author(@Args("id", { type: () => Int }) id: number) {
    return this.authorsService.findOne(id);
  }

  @Mutation(() => Author)
  createAuthor(@Args("input") input: CreateAuthorInput) {
    return this.authorsService.create(input);
  }

  // resolve a nested field efficiently (avoids N+1 with DataLoader)
  @ResolveField(() => [Post])
  posts(@Parent() author: Author) {
    return this.postsService.findByAuthor(author.id);
  }
}
```

**Key point:** with the code-first approach you define `@ObjectType`/`@Field` classes and `@Resolver`s (with `@Query`, `@Mutation`, `@ResolveField`) and Nest auto-generates the schema — reuse services/DI, and use DataLoader in field resolvers to avoid N+1 queries.
