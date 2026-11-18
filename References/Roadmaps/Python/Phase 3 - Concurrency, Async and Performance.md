# Phase 3: Concurrency, Async and Performance

Part of [[Python Roadmap - Index|Senior Python Developer Roadmap]]. Previous: [[Phase 2 - Typing, Testing and Tooling]]. Next: [[Phase 4 - Architecture, APIs and Data]].

**Duration:** Weeks 5–6
**Objective:** Choose the right concurrency model for a given workload and diagnose real performance problems.

## Week 5: Concurrency Models

### The GIL and Its Implications

- [ ] Understand what the Global Interpreter Lock actually prevents and permits.
- [ ] Understand why I/O-bound work benefits from threading/asyncio despite the GIL.
- [ ] Understand why CPU-bound work needs multiprocessing (or native extensions) to scale.
- [ ] Understand the free-threaded (no-GIL) build's status and implications at a conceptual level.

### Threading and Multiprocessing

- [ ] `threading.Thread`, `Lock`, `Event`, `Queue`.
- [ ] `concurrent.futures.ThreadPoolExecutor` for I/O-bound parallelism.
- [ ] `multiprocessing.Pool` / `ProcessPoolExecutor` for CPU-bound parallelism.
- [ ] Understand pickling constraints for multiprocessing arguments and return values.
- [ ] Race conditions, deadlocks, and how to avoid them.

### asyncio

- [ ] `async def`, `await`, and the event loop.
- [ ] `asyncio.gather`, `asyncio.TaskGroup`, and structured concurrency.
- [ ] `asyncio.Queue` for producer/consumer patterns.
- [ ] Cancellation and timeouts (`asyncio.wait_for`, `asyncio.timeout`).
- [ ] Common pitfalls: blocking calls inside async functions, forgetting to await.
- [ ] When to mix asyncio with a thread pool (`asyncio.to_thread`) for blocking calls.

### Practical Tasks

- [ ] Implement the same I/O-bound workload three ways: sequential, threaded, and asyncio — and compare wall-clock time.
- [ ] Implement a CPU-bound workload with `ProcessPoolExecutor` and measure the speedup.
- [ ] Build a small async producer/consumer pipeline using `asyncio.Queue`.
- [ ] Deliberately introduce and then fix a race condition using a lock.

**Deliverable:** The ability to pick the correct concurrency model for a workload and justify the choice with measurements.

## Week 6: Profiling and Performance Optimization

### Profiling

- [ ] `cProfile` and reading its output.
- [ ] `py-spy` for sampling production processes without code changes.
- [ ] `timeit` for microbenchmarks.
- [ ] `memory_profiler` / `tracemalloc` for memory usage.
- [ ] Reading flame graphs.

### Optimization Techniques

- [ ] Algorithmic complexity as the first lever, before micro-optimization.
- [ ] `functools.lru_cache` / `cache` for memoization.
- [ ] Avoiding unnecessary object creation in hot loops.
- [ ] Using built-in data structures (`collections.deque`, `set`) for the right access patterns.
- [ ] `__slots__` for memory-constrained object-heavy code.
- [ ] When a native extension (Cython, Rust via PyO3) is justified vs. premature.

### Practical Tasks

- [ ] Profile a deliberately slow function with `cProfile`, identify the bottleneck, and fix it.
- [ ] Benchmark two implementations of the same function with `timeit` and explain the difference.
- [ ] Use `tracemalloc` to find a memory growth issue in a long-running loop.
- [ ] Add `__slots__` to a high-volume class and measure the memory difference.

**Deliverable:** A performance analysis report showing a measured before/after improvement, not a guessed one.
