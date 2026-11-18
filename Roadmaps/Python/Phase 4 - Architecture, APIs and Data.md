---
tags: [roadmap, roadmap/python]
---

# Phase 4: Architecture, APIs and Data

Part of [[Python Roadmap - Index|Senior Python Developer Roadmap]]. Previous: [[Phase 3 - Concurrency, Async and Performance]]. Next: [[Phase 5 - Packaging, Deployment and Production Engineering]].

**Duration:** Weeks 7–8
**Objective:** Design maintainable services with clear boundaries and reliable data access.

## Week 7: Application Architecture and API Design

### Architecture

- [ ] Layered architecture: presentation, application/service, domain, data access.
- [ ] Dependency inversion and injecting dependencies rather than importing globals.
- [ ] Repository pattern for data access.
- [ ] Separating pure business logic from I/O.
- [ ] Module and package boundaries; avoiding circular imports.
- [ ] Configuration management (environment-based settings, secrets handling).

### API Design with FastAPI

- [ ] Path operations, request/response models with Pydantic.
- [ ] Dependency injection via `Depends`.
- [ ] Request validation and automatic OpenAPI documentation.
- [ ] Error handling with custom exception handlers.
- [ ] Middleware for cross-cutting concerns (logging, CORS, auth).
- [ ] Background tasks vs. a real task queue.

### Practical Tasks

- [ ] Structure a small service into layers (API, service, repository, domain).
- [ ] Build a FastAPI endpoint with a Pydantic request model, validation, and typed response.
- [ ] Implement a custom exception handler that maps domain errors to HTTP status codes.
- [ ] Write a dependency-injected service and test it with a fake repository.

**Deliverable:** A layered service with a documented, validated API surface.

## Week 8: Data Access and Persistence

### SQLAlchemy

- [ ] Core vs. ORM usage, and when to prefer each.
- [ ] Declarative models and relationships.
- [ ] Sessions, transactions, and the unit-of-work pattern.
- [ ] Query construction and avoiding N+1 queries.
- [ ] Connection pooling basics.
- [ ] Async SQLAlchemy with `asyncpg`.

### Migrations

- [ ] Alembic migration generation and review.
- [ ] Writing a manual migration for a non-trivial schema change.
- [ ] Migration rollback strategy.

### Data Integrity and Testing

- [ ] Transactions and rollback-on-error patterns.
- [ ] Testing against a real test database vs. mocking the data layer.
- [ ] Database fixtures and test isolation (transactional tests).
- [ ] Idempotency for retried operations.

### Practical Tasks

- [ ] Define SQLAlchemy models for the domain from Phase 1, with relationships.
- [ ] Generate and review an Alembic migration.
- [ ] Write repository tests against a real (containerized) test database.
- [ ] Identify and fix an N+1 query in a sample endpoint.

**Deliverable:** A complete, tested data access layer backing the service built in Week 7.
