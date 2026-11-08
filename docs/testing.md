# Testing

```bash
npx vitest run app/services/commentService.test.ts   # single file
npx vitest run -t "name"    # single test by name
```

Service tests use an in-memory SQLite DB built from the real Drizzle migrations (`app/test/setup.ts`). The pattern:

```ts
let testDb: ReturnType<typeof createTestDb>;
vi.mock("~/db", () => ({ get db() { return testDb; } }));
// import the service AFTER the mock
beforeEach(() => { testDb = createTestDb(); base = seedBaseData(testDb); });
```

Because tests run the migrations, a schema change needs `npm run db:generate` before tests can see it.

Reference example: `app/services/commentService.test.ts`.
