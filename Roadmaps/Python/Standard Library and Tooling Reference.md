---
tags: [roadmap, roadmap/python]
---

# Standard Library and Tooling Reference

Part of [[Python Roadmap - Index|Senior Python Developer Roadmap]]. A quick-lookup table; the phase notes cover the *why* behind each tool.

| Category | Module / Tool | Purpose |
|---|---|---|
| Data structures | `collections` (`deque`, `defaultdict`, `Counter`, `namedtuple`) | Specialized containers |
| Iteration | `itertools` | Efficient iterator building blocks |
| Functional | `functools` (`lru_cache`, `partial`, `reduce`, `wraps`) | Function composition and caching |
| Dataclasses | `dataclasses` | Boilerplate-free value classes |
| Typing | `typing` / `typing_extensions` | Static type annotations |
| Validation | `pydantic` | Runtime-validated models |
| Paths | `pathlib` | Object-oriented filesystem paths |
| Dates | `datetime` (+ `zoneinfo`) | Timezone-aware date/time handling |
| Concurrency | `asyncio` | Single-threaded cooperative concurrency |
| Concurrency | `concurrent.futures` | Thread/process pool executors |
| Concurrency | `multiprocessing` | True parallelism for CPU-bound work |
| Debugging | `pdb` / `breakpoint()` | Interactive debugger |
| Profiling | `cProfile`, `timeit`, `tracemalloc` | CPU and memory profiling |
| Testing | `pytest`, `unittest.mock` | Test framework and mocking |
| Env/config | `os.environ`, `pydantic-settings` | Configuration management |
| Serialization | `json`, `pickle` (trusted data only) | Data interchange |
| Logging | `logging` / `structlog` | Application logging |
| CLI | `argparse`, `click`, `typer` | Command-line interfaces |
| Packaging | `pyproject.toml`, `build`, `twine` | Build and publish packages |
| Linting/formatting | Ruff | Fast lint + format in one tool |
| Type checking | `mypy` / `pyright` | Static type verification |
| Dependency mgmt | `uv` / Poetry | Lockfiles and environment management |
