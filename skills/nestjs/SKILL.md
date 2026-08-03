---
name: nestjs
description: "Apply these opinionated NestJS conventions whenever writing or reviewing a NestJS backend: module boundaries and what to export, breaking circular imports without forwardRef, keeping logic in services, DTOs with class-validator behind a whitelisting ValidationPipe, response DTOs so entities never leak, picking correctly between guards/interceptors/pipes/filters, and validated ConfigModule."
---

# NestJS

House conventions for NestJS backends. Apply them to code you are writing or changing — don't restructure untouched modules unless asked.

## Conventions

- **A module owns one domain** and exports only what other modules legitimately need. A provider that isn't exported can be refactored freely; one that is becomes public API.
- **A circular import between modules is a design signal, not a `forwardRef` problem.** `forwardRef` makes it compile and leaves the cycle. Extract the shared piece into its own module instead.
- **Controllers translate HTTP; services hold the logic.** A controller that branches on business rules can't be reused by a job, a CLI, or a queue consumer, and its tests need an HTTP layer to say anything.
- **Every request body, query, and param goes through a DTO with `class-validator`**, behind a global `ValidationPipe` with `whitelist: true`, `forbidNonWhitelisted: true`, `transform: true`. Whitelisting is the part that matters: without it, an unexpected property rides through into your persistence layer.
- **`@ValidateNested()` needs `@Type(() => Child)` beside it.** class-transformer can't infer the target class from the TypeScript type, so without `@Type` the nested object stays a plain object and its rules never run — the request passes validation while carrying unvalidated data. Same for arrays, with `{ each: true }`.
- **Take `PartialType`/`OmitType`/`PickType` from `@nestjs/swagger`**, not `@nestjs/mapped-types`. Both exist and both compile; the mapped-types version silently drops the `@ApiProperty` metadata, so derived DTOs vanish from your OpenAPI schema.
- **A request-scoped provider makes every consumer request-scoped.** The scope propagates up the injection chain, so one `Scope.REQUEST` service quietly turns a tree of singletons into per-request instantiation. Reach for it only when you genuinely need per-request state, and know what it drags with it.
- **Response DTOs are what leaves the process.** Returning an entity directly leaks whatever a future migration adds to the table — password hashes, internal flags, soft-delete columns — with no code change to notice.
- **The right primitive for the concern.** Guards decide access, interceptors shape the request/response cycle, pipes transform and validate input, filters map exceptions to responses. A guard doing transformation runs at the wrong point in the lifecycle and won't see what it expects.
- **Throw the framework's HTTP exceptions** (`NotFoundException`, `ConflictException`, …). A bare `Error` becomes a 500, so a legitimate "not found" reads as an outage in your alerting.
- **`ConfigModule` with a validated schema, injected via `ConfigService`.** Reading `process.env` inside a service makes the value untestable and defers a missing-config failure to whenever that line first runs — usually in production.
- **Swagger decorators on every endpoint** (`@ApiOperation`, `@ApiResponse`). The generated spec is what clients build against; an undocumented endpoint is one nobody can consume without reading your source.
- **Tests: see the `testing` skill's NestJS Jest references** for structure, mocking, and assertion rules.
