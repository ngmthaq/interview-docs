# 21. How do you test a NestJS application? (Senior)

Nest ships with **`@nestjs/testing`**, which builds a **testing module** so you can instantiate providers with mocked dependencies.

**Unit test** — service with a mocked repository:

```ts
describe("UsersService", () => {
  let service: UsersService;
  const repo = { find: jest.fn(), save: jest.fn() };

  beforeEach(async () => {
    const module = await Test.createTestingModule({
      providers: [UsersService, { provide: getRepositoryToken(User), useValue: repo }],
    }).compile();

    service = module.get(UsersService);
  });

  it("returns all users", async () => {
    repo.find.mockResolvedValue([{ id: 1 }]);
    expect(await service.findAll()).toHaveLength(1);
  });
});
```

**E2E test** — with `supertest` against the full app:

```ts
const moduleRef = await Test.createTestingModule({ imports: [AppModule] }).compile();
const app = moduleRef.createNestApplication();
await app.init();
await request(app.getHttpServer()).get("/users").expect(200);
```

**Key point:** use `Test.createTestingModule` to assemble providers with mocked dependencies for unit tests, and build a full `createNestApplication()` + `supertest` for E2E tests — DI makes swapping real deps for mocks trivial.
