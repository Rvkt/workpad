# Phase 2: Typing, Testing and Tooling

Part of [[Python Roadmap - Index|Senior Python Developer Roadmap]]. Previous: [[Phase 1 - Core Language and Idiomatic Python]]. Next: [[Phase 3 - Concurrency, Async and Performance]].

**Duration:** Weeks 3–4
**Objective:** Build type-safe, well-tested code with a reliable tooling baseline.

## Week 3: Static Typing and Pydantic

### Type Hints

- [ ] Basic type hints for variables, functions, and return types.
- [ ] Generics with `TypeVar` and `Generic`.
- [ ] `Optional`, `Union`, and the `X | Y` syntax.
- [ ] `Literal`, `TypedDict`, and `NamedTuple`.
- [ ] `Protocol` for structural typing.
- [ ] `overload` for functions with multiple valid signatures.
- [ ] Type narrowing and `TypeGuard`.
- [ ] Running mypy or pyright and resolving real type errors, not just suppressing them.

### Pydantic and Runtime Validation

- [ ] Define models with Pydantic.
- [ ] Field validation and custom validators.
- [ ] Nested models and model composition.
- [ ] Serialization to/from JSON and dict.
- [ ] Settings management with `pydantic-settings`.
- [ ] Understand the difference between static typing (compile-time) and Pydantic validation (runtime).

### Practical Tasks

- [ ] Add full type hints to the Phase 1 domain model and get a clean mypy/pyright run.
- [ ] Convert a dataclass-based model to Pydantic and add field validators.
- [ ] Write a `Protocol` for a plugin interface and implement two conforming classes.
- [ ] Set up a typed settings class loaded from environment variables.

**Deliverable:** A fully typed, validated codebase that catches real bugs before runtime.

## Week 4: Testing and Developer Tooling

### pytest Fundamentals

- [ ] Test discovery and naming conventions.
- [ ] Fixtures, including scoped fixtures (`function`, `module`, `session`).
- [ ] Parametrized tests.
- [ ] `pytest.raises` for exception testing.
- [ ] Mocking with `unittest.mock` / `pytest-mock`.
- [ ] Measuring coverage with `pytest-cov` and interpreting the report meaningfully.

### Advanced Testing

- [ ] Property-based testing with Hypothesis.
- [ ] Testing async code with `pytest-asyncio`.
- [ ] Test doubles: mocks vs. stubs vs. fakes, and when each is appropriate.
- [ ] Avoiding brittle tests that over-mock internal implementation details.

### Tooling and Automation

- [ ] Configure Ruff for linting and formatting.
- [ ] Configure pre-commit hooks for lint, format, and type-check.
- [ ] Set up `pyproject.toml` as the single project configuration file.
- [ ] Understand virtual environments and why global installs are avoided.
- [ ] Set up uv or Poetry for dependency management.

### Practical Tasks

- [ ] Write a full pytest suite for the Phase 1/2 domain model, including parametrized and exception-path tests.
- [ ] Add a property-based test for a pure function using Hypothesis.
- [ ] Configure pre-commit with Ruff and mypy, and verify it blocks a deliberately broken commit.
- [ ] Measure and improve coverage on a previously untested module.

**Deliverable:** A reliable, automated quality baseline: typed, tested, linted, and enforced on every commit.
