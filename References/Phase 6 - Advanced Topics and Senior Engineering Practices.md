# Phase 6: Advanced Topics and Senior Engineering Practices

Part of [[Python Roadmap - Index|Senior Python Developer Roadmap]]. Previous: [[Phase 5 - Packaging, Deployment and Production Engineering]].

**Duration:** Weeks 11–12
**Objective:** Round out advanced language features and apply senior-level engineering judgment.

## Week 11: Advanced Language Features

### Metaprogramming

- [ ] Metaclasses and when they're actually warranted (rarely).
- [ ] `__init_subclass__` as a lighter alternative to metaclasses.
- [ ] Class decorators.
- [ ] `exec` / `eval` risks and why they're avoided in most production code.

### Advanced Typing

- [ ] Generic classes and bounded TypeVars.
- [ ] `ParamSpec` for decorator typing.
- [ ] Variance (covariance/contravariance) at a conceptual level.
- [ ] Type stubs (`.pyi` files) for untyped third-party libraries.

### Memory and Object Model Internals

- [ ] Reference counting and garbage collection basics.
- [ ] Weak references (`weakref`) and when they prevent memory leaks.
- [ ] Understanding why mutable default arguments are a common bug source.
- [ ] `copy` vs. `deepcopy` semantics.

### Practical Tasks

- [ ] Write a class decorator that registers subclasses in a plugin registry.
- [ ] Add type stubs for a small untyped third-party module used in the project.
- [ ] Deliberately create and then fix a mutable-default-argument bug.
- [ ] Use `weakref` to break a reference cycle in a cache implementation.

**Deliverable:** Comfort reading and occasionally writing advanced Python without reaching for it unnecessarily.

## Week 12: Senior Engineering Practices

### Code Review and Design

- [ ] Reviewing for correctness, readability, and maintainability — not just style.
- [ ] Identifying premature abstraction vs. genuine complexity.
- [ ] Writing RFCs/design docs for non-trivial changes.
- [ ] Trade-off analysis: documenting why an approach was chosen, not just what it does.

### Security

- [ ] Avoiding `pickle` on untrusted input.
- [ ] SQL injection prevention via parameterized queries.
- [ ] Dependency vulnerability scanning as a routine practice.
- [ ] Secrets management (never hardcoded, never logged).
- [ ] Input validation at system boundaries.

### Debugging Production Issues

- [ ] Reading a stack trace methodically, from the bottom up.
- [ ] Using `pdb` / `breakpoint()` effectively.
- [ ] Reproducing a production bug locally with minimal data.
- [ ] Using logs and traces to narrow down an issue before touching code.
- [ ] Writing a regression test before fixing the bug.

### Practical Tasks

- [ ] Review a peer's (or your own past) code and write structured feedback distinguishing blocking issues from suggestions.
- [ ] Write a short design doc for a non-trivial change to the service built in Phases 4–5.
- [ ] Deliberately reproduce and fix a bug using `pdb`, writing a regression test first.
- [ ] Run a dependency and code security scan on the full project and address findings.

**Deliverable:** Demonstrated senior-level judgment: a reviewed design doc, a security-audited codebase, and a debugged production-style issue with a regression test.
