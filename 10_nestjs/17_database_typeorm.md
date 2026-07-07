# 17. How do you integrate a database (TypeORM)? (Mid)

Nest offers first-class integrations via `@nestjs/typeorm` (also Prisma, Mongoose, MikroORM). TypeORM uses **entities** and **repositories**.

```ts
// entity
@Entity()
export class User {
  @PrimaryGeneratedColumn() id: number;
  @Column() name: string;
  @Column({ unique: true }) email: string;
}

// module
@Module({
  imports: [TypeOrmModule.forFeature([User])], // register the repository
  providers: [UsersService],
})
export class UsersModule {}

// service — inject the repository
@Injectable()
export class UsersService {
  constructor(@InjectRepository(User) private usersRepo: Repository<User>) {}

  findAll() {
    return this.usersRepo.find();
  }
  create(dto: CreateUserDto) {
    return this.usersRepo.save(this.usersRepo.create(dto));
  }
}
```

Root connection: `TypeOrmModule.forRoot({...})` (or `forRootAsync` to pull config from `ConfigService`).

**Key point:** register the ORM once with `forRoot`/`forRootAsync`, expose entity repositories per feature with `forFeature`, and inject them via `@InjectRepository` into services — keeping data access in the repository/service layer.
