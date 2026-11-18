# Phase 1: Core Language and Idiomatic Python

Part of [[Python Roadmap - Index|Senior Python Developer Roadmap]]. Next: [[Phase 2 - Typing, Testing and Tooling]].

**Duration:** Weeks 1–2
**Objective:** Build fluency with Python's data model and idiomatic patterns beyond basic syntax.

## Week 1: Data Model and Core Idioms

### The Data Model

- [ ] Understand dunder methods and how `len()`, `str()`, `in`, and `[]` dispatch to them.
- [ ] Understand `__init__` vs. `__new__`.
- [ ] Understand `__repr__` vs. `__str__`.
- [ ] Understand iterables, iterators, and `__iter__` / `__next__`.
- [ ] Understand context managers and `__enter__` / `__exit__`.
- [ ] Understand descriptors at a conceptual level.
- [ ] Understand mutable vs. immutable types and reference semantics.

### Idiomatic Python

- [ ] List, dict, and set comprehensions.
- [ ] Generator expressions and `yield`.
- [ ] Unpacking, starred expressions, and multiple assignment.
- [ ] `enumerate`, `zip`, and `itertools` basics.
- [ ] f-strings and string formatting conventions.
- [ ] Context managers via `with`, including `contextlib.contextmanager`.
- [ ] EAFP vs. LBYL and when each is appropriate.

### Practical Tasks

- [ ] Implement a custom iterable class.
- [ ] Implement a custom context manager using `contextlib.contextmanager`.
- [ ] Refactor a loop-heavy script into comprehensions and generator expressions.
- [ ] Write a small CLI script using only the standard library.

**Deliverable:** Comfortable reading and writing idiomatic Python, and understanding why it looks the way it does.

## Week 2: OOP, Functional Patterns and Error Handling

### Object-Oriented Python

- [ ] Classes, inheritance, and MRO (method resolution order).
- [ ] `@dataclass` and when to prefer it over a plain class.
- [ ] `@property` for computed attributes.
- [ ] Class methods, static methods, and when each is appropriate.
- [ ] Composition over inheritance.
- [ ] Protocols and structural typing (`typing.Protocol`).
- [ ] Abstract base classes (`abc.ABC`).

### Functional Patterns

- [ ] First-class functions and closures.
- [ ] `functools.partial`, `functools.reduce`, `functools.lru_cache`.
- [ ] Decorators: writing and understanding them, including those that take arguments.
- [ ] `functools.wraps` and why it matters for decorators.

### Error Handling

- [ ] Exception hierarchy and custom exception classes.
- [ ] `try` / `except` / `else` / `finally` semantics.
- [ ] Exception chaining (`raise ... from ...`).
- [ ] Exception groups (`except*`) for structured concurrent error handling.
- [ ] When to catch broadly vs. narrowly.

### Practical Tasks

- [ ] Implement a small library of dataclasses representing a domain model.
- [ ] Write a parameterized decorator (e.g. a retry decorator with configurable attempts).
- [ ] Design a custom exception hierarchy for an application.
- [ ] Refactor inheritance-heavy code into composition.

**Deliverable:** A reusable domain model and decorator library demonstrating idiomatic OOP and functional patterns.
