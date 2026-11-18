Part of [[Python Roadmap - Index|Python Mastery Roadmap]].

# Python Notes (Explained Simply)

These are plain-English study notes to go along with the roadmap. The roadmap tells you *what* to check off. This file tries to explain *what the ideas actually mean*, using everyday language instead of jargon. Where a technical word has to appear, it's explained right next to it.

---

## Phase 1: Core Language and Idiomatic Python

### What "the data model" really means

Python has a set of special methods with double underscores, like `__init__` or `__len__` (people call these "dunder methods," short for "double underscore"). These are hooks that let your own objects plug into Python's built-in behavior. For example, when you write `len(my_list)`, Python is secretly calling `my_list.__len__()`. If you build your own class and give it a `__len__` method, then `len()` will work on your objects too. The big idea: Python's built-in operators and functions (`len()`, `in`, `[]`, `str()`) are really just polite ways of asking an object "can you tell me your length?" or "can you turn yourself into a string?" If you teach your class how to answer, it behaves like a native Python type.

`__init__` sets up an object after it already exists (filling in its fields). `__new__` is rarer — it's the step that actually creates the object in memory, before `__init__` touches it. Think of `__new__` as the factory building an empty box, and `__init__` as the person putting stuff inside the box.

`__repr__` and `__str__` both turn an object into text, but for different audiences. `__str__` is for people — a friendly description. `__repr__` is for developers debugging in a terminal — precise enough that, ideally, you could copy it and recreate the object.

An "iterable" is anything you can loop over with `for item in thing`. An "iterator" is the actual helper object that remembers where you are in that loop and hands out one item at a time when asked. Lists are iterable, but they're not iterators themselves — Python creates an iterator behind the scenes to walk through them.

A "context manager" is anything you use with the `with` keyword, like `with open("file.txt") as f:`. It guarantees cleanup happens even if something goes wrong inside — in this example, that the file gets closed no matter what. `__enter__` runs at the start of the `with` block, and `__exit__` runs at the end, even if there was an error in between. It's like checking into a hotel room (`__enter__`) and the hotel guaranteeing someone checks you out and locks up (`__exit__`) even if you leave in a hurry.

"Descriptors" are an advanced mechanism behind things like `@property` — they let you control what happens when an attribute is read or set on an object, without the caller noticing anything unusual. You don't need to master writing your own descriptors early on; just know that some "magic" attribute behavior in Python is powered by this.

"Mutable vs immutable" is about whether a value can be changed after it's created. A list is mutable — you can add or remove items from it in place. A string or a tuple is immutable — once made, it can't be altered; any "change" actually creates a brand-new object. This matters because if two variables point to the same mutable object, changing it through one variable changes what the other variable sees too. This is "reference semantics": a variable isn't a box holding a value, it's more like a sticky note pointing at a box. Two sticky notes can point at the same box.

### Writing Python the "idiomatic" way

"Idiomatic" just means writing code the way experienced Python users would write it, following the language's natural style, rather than writing Python like it's another language (for example, writing C-style `for i in range(len(list))` loops when you could just loop directly over the items).

A "comprehension" is a compact way to build a list, dict, or set in one line, instead of writing a multi-line loop with `.append()`. For example, `[x * 2 for x in numbers]` means "give me a new list where every number is doubled." It reads almost like English once you get used to it.

A "generator expression" looks similar but doesn't build the whole list in memory at once — it produces items one at a time, on demand, as you ask for them. This matters for big data: a generator can process a huge file without ever loading the whole thing into memory. `yield` is the keyword that turns a normal function into a generator — instead of returning one value and ending, the function can pause, hand back a value, and resume later exactly where it left off.

"Unpacking" means pulling values out of a list or tuple into separate variables in one line, like `a, b = (1, 2)`. "Starred expressions" (`*rest`) let you grab "everything else" into a list, like `first, *rest = [1, 2, 3, 4]`, where `rest` becomes `[2, 3, 4]`.

`enumerate` gives you both the index and the value while looping, so you don't have to manually track a counter. `zip` lets you loop over two lists side by side, pairing up matching items. `itertools` is a standard library toolbox full of small, efficient looping helpers (like chaining lists together or generating combinations) so you don't have to write that logic by hand.

f-strings are the modern way to build strings with variables inside them, like `f"Hello {name}"` — much easier to read than older string-formatting methods.

EAFP stands for "Easier to Ask Forgiveness than Permission" — it means: just try the thing, and if it fails, catch the error. LBYL stands for "Look Before You Leap" — it means: check if something is safe first, then do it. Python generally favors EAFP: for example, trying to access a dictionary key and catching the error if it's missing, rather than first checking "does this key exist?" and then accessing it. This matters because checking-then-acting can have a timing gap where things change between the check and the action; trying-and-catching is often safer and simpler.

### Object-oriented and functional ideas

"MRO" (method resolution order) is the order Python searches through a class and its parent classes to find a method when you call it. This mostly matters when a class inherits from multiple other classes, and you need to know which version of a method actually runs.

`@dataclass` is a shortcut for writing simple classes that mostly just hold data (like a `Point` with `x` and `y`). Instead of manually writing `__init__`, `__repr__`, and equality checks, you just declare the fields and Python writes that boilerplate for you.

`@property` lets you make a method behave like it's just a plain attribute. For example, you could store `radius` on a `Circle` object but compute `area` on the fly every time someone asks for it, while it still looks like `circle.area` instead of `circle.area()`.

"Composition over inheritance" is a design principle: instead of building deep family trees of classes (`Dog` inherits from `Animal` inherits from `LivingThing`...), it's often simpler and more flexible to build objects out of smaller pieces that work together, the way a car is built from an engine, wheels, and a chassis, rather than being a a special kind of "VehicleBase." Inheritance can get rigid and confusing when it goes too many layers deep; composition tends to stay easier to change later.

A "protocol" is a way of saying "I don't care what class this object is, I just care whether it has the methods I need." This is called "structural typing" — if it walks like a duck and quacks like a duck, Python treats it as a duck, regardless of its actual family tree. An "abstract base class" is similar but stricter — it's a parent class that says "any class that inherits from me MUST implement these specific methods," and Python will refuse to create an object if those methods are missing.

A "closure" is a function that remembers variables from the place it was created, even after that outer code has finished running. It's like a backpack a function carries around with it, filled with values it needs later. Decorators often rely on closures.

A "decorator" is a function that wraps another function to add extra behavior without changing the original function's code — like putting a function inside a gift box that adds something (logging, timing, retrying) before or after the original runs. `functools.wraps` is a small but important detail: without it, a decorated function loses its original name and documentation, which makes debugging confusing; `wraps` preserves that information.

### Handling errors well

Exceptions are Python's way of saying "something went wrong, and normal execution can't continue." A "custom exception class" lets you create your own named error types (like `InsufficientFundsError`) instead of using generic built-in ones, so the error message in your code is self-explanatory.

`try`/`except`/`else`/`finally` is a structured way to say: "try this; if it fails in this specific way, do that instead; if it succeeded, do this other thing; and no matter what happened, always do this cleanup step at the end."

"Exception chaining" (`raise ... from ...`) lets you say "this new error happened, and here's the original error that caused it," so when debugging you can see the whole chain of cause and effect instead of losing the original problem.

"Exception groups" are a newer feature for when multiple things can fail at once — for example, in concurrent code where several tasks run in parallel and more than one might fail simultaneously. Instead of only being able to report one error, Python can now report several at once, bundled together.

The general rule on catching errors: catch narrowly (specific error types) when you know exactly what might go wrong and how to handle it, and avoid catching broad, generic errors, because that can silently hide real bugs you didn't anticipate.

---

## Phase 2: Typing, Testing and Tooling

### Why add type hints to Python at all

Python normally doesn't force you to declare what type a variable is — you can put a number in a variable and later put a string in the same variable. Type hints are an optional layer on top that let you write down your intentions, like `def add(a: int, b: int) -> int:`, meaning "this function expects two whole numbers and returns a whole number." Python itself still won't stop you at runtime if you break that promise, but a separate tool (like mypy or pyright) can read your code and warn you ahead of time if you're about to pass the wrong kind of value somewhere. Think of type hints as leaving clear labels on boxes so that anyone (including future you) can tell what's supposed to go inside, and a checker tool that walks around double-checking every box has the right contents before you ship anything.

`Optional` and `Union` describe a value that could be one of several types — for example, "this function might return a number, or it might return nothing (`None`)." The newer `X | Y` syntax is just a shorter way of writing "either X or Y."

`Literal` lets you say a value must be one of a few exact, fixed options, like `"small" | "medium" | "large"` rather than any string. `TypedDict` lets you describe the exact expected shape of a dictionary, as if it were a lightweight data class. `NamedTuple` is similar — a tuple where each slot also has a name, like `Point(x, y)`, so you can write `point.x` instead of `point[0]`.

Generics (`TypeVar`, `Generic`) let you describe "a container of some type T" without saying in advance what T is — like saying "a box that holds exactly one kind of thing, I just don't know which kind yet until you tell me." A list of integers and a list of strings use the same `List` idea, generically parameterized by what's inside.

`overload` lets you describe a function that behaves differently (returns different types) depending on what kind of input it gets, while still giving accurate type information for each case.

"Type narrowing" is when a type checker gets smarter about a variable's type based on a check you just performed — for example, after you check `if value is not None:`, the checker now treats `value` as definitely not `None` for the rest of that block. `TypeGuard` lets you write your own custom checks that teach the type checker how to narrow types in more complex situations.

A key distinction: static typing (mypy/pyright) is checked before your code even runs, by reading the source code. Pydantic validation happens at runtime, actually inspecting real data as it flows through your program (for example, validating that JSON coming from a user actually has the fields and types you expect). Static typing catches mistakes in your own code's logic; Pydantic catches bad data coming from the outside world, which static typing can't see coming.

### Pydantic in plain terms

Pydantic lets you define a "model" — basically a class describing the exact shape of some data (a `User` with a `name: str` and `age: int`, for example). When you create data through a Pydantic model, it automatically checks that each field matches what you said it should be, and it will raise a clear error if, say, someone tries to put text into an age field. This is enormously useful at the edges of your system — like when you receive an API request — because external data can never be trusted to arrive in the shape you expect. Pydantic models can also nest inside each other (a model containing another model) and can convert themselves to and from JSON easily, which is why they're so popular for APIs. `pydantic-settings` extends this idea to application configuration, letting you define what settings your app needs and have them automatically loaded and validated from environment variables.

### Testing: why and how

A test is just a small program that checks whether another piece of your code behaves correctly. Pytest is the most popular tool in Python for writing and running tests. "Test discovery" means pytest automatically finds files and functions that look like tests (usually named `test_*.py` and functions starting with `test_`) without you having to list them all manually.

A "fixture" is reusable setup code for tests — for example, creating a fake database connection that several tests need. Instead of repeating that setup in every test, you define it once as a fixture and tests can just ask for it. "Scoped" fixtures control how often that setup re-runs: a `function`-scoped fixture resets for every single test, while a `session`-scoped fixture is created once and shared across the whole test run (useful for things that are expensive to set up).

"Parametrized tests" let you run the same test logic repeatedly with different sets of input values, so you don't have to copy-paste nearly-identical tests just to try different numbers.

`pytest.raises` is how you test that your code correctly raises an error when it's supposed to — you're testing that bad input actually gets rejected, not just that good input works.

"Mocking" means replacing a real piece of your code (often something slow or external, like a network call) with a fake stand-in during a test, so you can test your logic in isolation without actually hitting the network, database, etc. A "mock" generally just records what was called and lets you assert on it. A "stub" returns canned, pre-set answers. A "fake" is a simplified-but-working version of the real thing (like an in-memory database standing in for a real one). The warning about "over-mocking" is important: if you fake out too much of your own code's internal plumbing, your tests start checking "did I call things in the exact way I wrote them" rather than "does this actually produce the right result" — which makes tests brittle and not very useful.

"Coverage" measures what percentage of your code actually gets executed by your tests. It's a useful signal for finding completely untested code, but a high percentage doesn't by itself prove your tests are actually any good — you can "cover" a line of code without meaningfully checking its behavior.

"Property-based testing" (via a tool called Hypothesis) flips normal testing around: instead of you picking a few example inputs to test, you describe a *property* that should always hold true (like "sorting a list twice gives the same result as sorting it once"), and the tool automatically generates lots of random and edge-case inputs trying to break that property. It's great at finding weird edge cases humans don't think to test.

### Tooling that keeps quality consistent

Ruff is a fast tool that checks your code for style issues and common mistakes (linting) and can also auto-format your code to a consistent style. "Pre-commit hooks" are automated checks that run right before you're allowed to save (commit) a change in git — so if your code fails linting, formatting, or type-checking, the commit is blocked until you fix it, catching mistakes before they ever reach the rest of the team.

`pyproject.toml` is becoming the single standard configuration file for a Python project — instead of scattering settings for your dependencies, linter, formatter, and type checker across many different files, they increasingly all live in this one file.

A "virtual environment" is an isolated folder containing its own copy of Python packages for one specific project, so that different projects on your machine don't fight over conflicting package versions. Installing packages "globally" (shared by your whole computer) risks one project's dependencies silently breaking another project's. Tools like uv or Poetry manage these environments and your project's dependency list for you, generating a "lockfile" that records the exact versions used so the project installs identically on any machine.

---

## Phase 3: Concurrency, Async and Performance

### The GIL, explained simply

Python has something called the Global Interpreter Lock, or GIL. In plain terms: in the standard version of Python, only one thread can actually be executing Python code at any single instant, even if your computer has many CPU cores. It's like a single-lane bridge — multiple cars (threads) can be waiting to cross, but only one is actually on the bridge moving at a time.

This sounds bad, but it doesn't make threads useless. If your program spends most of its time waiting — for a web request to come back, for a file to finish reading from disk — that's called "I/O-bound" work (I/O meaning input/output, i.e., talking to the outside world). During that waiting time, the GIL gets released, so other threads can run. This means threads (and `asyncio`, discussed below) can dramatically help when your program is mostly waiting around, even though only one is ever truly "computing" at once.

But if your work is "CPU-bound" — meaning the computer is genuinely crunching numbers nonstop, not waiting on anything — threads don't help, because that single-lane bridge rule means only one thread's calculations can run at a time regardless of how many threads you create. For true CPU-bound parallelism, you need multiprocessing instead: running entirely separate Python processes, each with its own GIL, so they can genuinely use multiple CPU cores simultaneously. The cost is that separate processes don't share memory directly, so passing data between them has overhead.

There's ongoing work on a "free-threaded" (no-GIL) version of Python that removes this single-lane restriction, but it's still maturing — the main thing to know conceptually is that it would let threads do true CPU parallel work too.

### Threads, processes, and asyncio

A "thread" is a lightweight unit of execution inside a program; several threads can share the same memory. A "process" is a full separate running copy of the program, with its own isolated memory. `Lock`, `Event`, and `Queue` are tools to help threads coordinate and avoid messing with shared data at the same time; a `Lock` is like a bathroom door lock — only one thread can hold it at a time, so others wait their turn instead of all barging in together.

`ThreadPoolExecutor` gives you a ready-made pool of worker threads for I/O-bound tasks, so you don't have to manage thread creation and cleanup yourself. `ProcessPoolExecutor` / `multiprocessing.Pool` does the equivalent for CPU-bound tasks using separate processes. Because processes don't share memory, any data you send to or receive from a worker process has to be "pickled" — converted into a format that can be transmitted and reconstructed — which means not every kind of Python object can be sent that way (for example, you generally can't send things like open file handles or live network connections across processes).

A "race condition" happens when two threads read and modify shared data at almost the same time in a way that produces wrong, unpredictable results, because the timing of who-does-what-first wasn't controlled. A "deadlock" happens when two threads each wait forever for a lock the other one is holding, so neither can proceed — like two people each waiting for the other to go first through a door, forever.

`asyncio` is a different approach: instead of using real OS threads, a single thread runs many tasks that cooperatively pause and resume. `async def` marks a function as one that can pause partway through; `await` is the pause point, usually while waiting on something slow like a network call. The "event loop" is the manager that keeps track of all these paused tasks and decides which one gets to resume next once its wait is over. This is efficient for handling thousands of things waiting on network calls at once, with much less overhead than creating thousands of real threads.

`asyncio.gather` and `TaskGroup` let you run several async tasks concurrently and wait for all of them to finish. "Structured concurrency" is a design idea that says: all the concurrent tasks you start inside a block should be guaranteed to finish (or be properly cancelled) before that block exits — no orphaned tasks left running unmanaged in the background. Cancellation and timeouts let you say "give up waiting on this after N seconds" so a slow or hung operation doesn't block everything else forever.

A classic pitfall: calling a slow, blocking (non-async) function from inside async code freezes the entire event loop, stalling every other task that was supposed to be running concurrently, because remember — it's all happening on effectively one thread taking turns. `asyncio.to_thread` is the fix: it lets you shove that one blocking call off onto a real separate thread so the event loop can keep servicing everything else while it waits.

### Profiling and performance: measure before you touch anything

Profiling means actually measuring where your program's time (or memory) is going, instead of guessing. `cProfile` runs your code and records how much time was spent inside every function, so you can see exactly which part is slow. `py-spy` can attach to an already-running Python process (even in production) and sample what it's doing, without needing to change any code or restart it — useful when you can't just stop a live service to add profiling code. `timeit` is for small, precise comparisons — timing a tiny snippet of code very accurately, useful for comparing "which of these two approaches is faster" on a small scale. `tracemalloc` and `memory_profiler` track memory usage over time, which helps when a program's memory keeps growing (a "memory leak") and you need to find what's holding onto all that memory.

A "flame graph" is a visual way of representing profiling data — wider sections represent more time spent, and stacked sections show which function called which, making it easy to spot the one function eating most of the time at a glance.

On actually making things faster: the single biggest lever is almost always the algorithm itself — choosing a fundamentally better approach (for example, looking something up in a set, which is close to instant, instead of scanning through a list one by one) beats any amount of fiddly micro-optimization. `functools.lru_cache` memoizes a function, meaning it remembers past results for past inputs and returns the cached answer instantly instead of recomputing, which is valuable when the same expensive calculation gets repeated with the same inputs.

`collections.deque` is a list-like structure optimized for adding/removing items from both ends efficiently, useful for queues. Choosing the right data structure for what you're actually doing with it (fast lookup needs a set or dict, fast ordered insertion at both ends needs a deque) usually matters more than clever tricks.

`__slots__` is a way to tell Python "this class will only ever have these specific fields, don't allocate the usual flexible extra storage for arbitrary attributes" — this saves meaningful memory when you're creating huge numbers of small objects.

Reaching for a native extension (writing part of your code in a faster language like Rust or C, via tools like Cython or PyO3) is a serious, heavier step that's only worth it once you've already tried better algorithms and data structures and profiling shows a real, measured bottleneck that pure Python genuinely can't solve — doing it prematurely, before you've actually measured a problem, just adds complexity for no proven benefit.

---

## Phase 4: Architecture, APIs and Data

### Why structure an application into layers

As an application grows, mixing everything together (database calls, business rules, and web-handling code all tangled in the same function) becomes hard to change safely. "Layered architecture" is the idea of separating concerns into distinct layers: the presentation layer (handling incoming requests), the application/service layer (orchestrating what should happen), the domain layer (the core business rules, the "what this application is actually about"), and the data access layer (actually talking to the database). The value is that you can change how data is stored, or how requests come in, without having to rewrite your core business logic, because they're not tangled together.

"Dependency inversion" means a piece of code asks for what it needs to be handed in (injected) rather than reaching out and grabbing a specific global thing itself. For example, instead of a function directly importing and using one specific database connection, it accepts "a database connection" as a parameter. This makes it much easier to swap in a fake database during tests, because you just hand in a different thing satisfying the same shape, without changing the function's code at all.

The "repository pattern" means putting all the code that knows how to fetch/save a particular kind of data behind one dedicated class (a `UserRepository`, say), so the rest of the application doesn't need to know or care whether that data lives in a SQL database, a document store, or a hard-coded list in memory — it just asks the repository for a user.

"Separating pure business logic from I/O" means keeping the core decision-making code (figuring out what should happen) separate from the actual act of talking to a database/file/network to make it happen. Pure logic is far easier to test, because you don't need a real database just to check that your discount calculation is correct.

"Circular imports" happen when module A imports something from module B, and module B tries to import something from module A, creating a loop Python can't resolve cleanly. Keeping clear one-directional boundaries between modules/packages avoids this tangled mess.

### Building an API (using FastAPI as the example)

A "path operation" is just the pairing of a URL (like `/users/5`) with an HTTP method (like GET or POST) and the function that handles it. FastAPI lets you describe the expected shape of the incoming request body and the outgoing response using Pydantic models, and it automatically checks incoming data against that shape, rejecting malformed requests before your own code even runs.

`Depends` is FastAPI's dependency injection system — a way of saying "before running this endpoint, go get me a database session (or the currently logged-in user, etc.) and hand it to my function," without the endpoint function needing to know exactly how that thing gets created.

FastAPI automatically generates interactive API documentation (OpenAPI/Swagger) directly from your type hints and models, so your documentation can't easily drift out of sync with your actual code, since it's generated from the same source.

A custom exception handler lets you catch your own application-specific errors (like "user not found") and automatically turn them into the correct HTTP status code and a clean error response, instead of leaking a raw, ugly server error to the caller.

"Middleware" is code that runs around every request, regardless of which specific endpoint is being hit — useful for cross-cutting concerns like logging every request, handling CORS (letting browsers from other websites call your API safely), or checking authentication.

"Background tasks" let an endpoint return a response quickly while some additional work (like sending a confirmation email) continues after the response is sent. A real task queue (a separate dedicated system for running jobs) is needed once background work becomes heavier, needs retries, or needs to survive the web server restarting — background tasks built into the web framework are meant for lightweight, best-effort work only.

### Working with databases

SQLAlchemy is the most common tool for talking to SQL databases from Python. "Core" is its lower-level interface where you write something closer to actual SQL queries using Python. The "ORM" (object-relational mapper) is a higher-level interface where you work with regular Python classes and objects, and SQLAlchemy translates your work with those objects into the SQL behind the scenes. The ORM is usually more convenient for typical application code; Core gives you more direct control when you need finely-tuned queries.

A "session" represents a working conversation with the database — a space where you gather up changes. A "transaction" is a group of changes that either all succeed together or all get rolled back together if something fails partway through, so your data never ends up in a half-finished, inconsistent state. The "unit of work" pattern just means: gather up all the changes you intend to make, then commit them together as one transaction.

An "N+1 query" problem is a common and costly mistake: you fetch a list of items (1 query), and then, for each item, you run another separate query to fetch related data (N more queries) — instead of fetching everything you need in a smarter, combined way. This can quietly turn a fast page into one that makes hundreds of unnecessary database round trips.

"Connection pooling" means the application keeps a reusable set of open database connections ready to go, rather than opening and closing a brand new connection for every single request, which would be slow.

Alembic is the standard tool for managing "migrations" — scripted, version-controlled changes to your database's structure (like adding a new column) so that every environment's database schema can be updated in a repeatable, trackable way, and so changes can be rolled back if something goes wrong.

"Idempotency" means designing an operation so that running it multiple times by accident (for example, due to a network retry) has the same end result as running it once — important for things like payment processing, where an accidental double-charge would be a real problem.

Testing against a real (but temporary, often containerized) test database is usually more trustworthy than mocking the database layer entirely, because mocks can't catch real SQL mistakes or constraint violations — but it's heavier to set up, so teams balance the two depending on what's being tested.

---

## Phase 5: Packaging, Deployment and Production Engineering

### Turning code into a shareable package

"Packaging" means organizing your code so it can be installed and reused elsewhere, the same way you install any library with `pip install something`. `pyproject.toml` has become the standard single file describing a Python project's metadata (its name, version, dependencies, and how to build it). A "build backend" (like Hatchling or setuptools) is the actual tool that knows how to turn your source code into installable packages.

A "wheel" and an "sdist" (source distribution) are the two common packaged formats a Python project gets built into — a wheel is a pre-built, ready-to-install format; an sdist is closer to raw source code that gets built at install time. "Publishing" a package (with a tool like `twine`) means uploading it somewhere others (or your own other projects) can install it from.

Semantic versioning is a widely-used convention for version numbers (like `2.3.1`) where each part of the number has a meaning: the first number changes for changes that could break existing users, the second for new features that don't break anything, and the third for small fixes. This lets other people reading your version number understand, at a glance, how risky it is to upgrade.

`__all__` and "avoiding leaking internals" is about being deliberate regarding what parts of your package are meant for outside use versus what's just internal implementation detail you might change later without warning. A clear public API is like a building's front door and reception desk — visitors use that, while the back-office machinery stays hidden and free to change without breaking anyone depending on it.

### Managing dependencies responsibly

A "lockfile" (like `uv.lock` or `poetry.lock`) records the exact, specific versions of every dependency (and the dependencies of your dependencies) that were actually used, so that installing the project later — on any machine — reproduces an identical environment. Without a lockfile, "it works on my machine" problems creep in because different installs might silently pick up newer versions of underlying packages.

Separating dependency groups (runtime vs. dev vs. optional) means the packages only needed for testing or development (like pytest) don't get installed in your actual production environment, keeping it lighter and reducing the surface area for security issues.

"Pinning" dependency versions means deciding how strictly you lock a dependency's version down. Exact pins (`package==1.2.3`) are the most reproducible but require manual effort to ever get security fixes or improvements. Compatible ranges (`package>=1.2,<2.0`) allow some automatic updates (like bug fixes) while still protecting against bigger, possibly breaking changes. Auditing dependencies means periodically checking whether any package you depend on has known security vulnerabilities or has been abandoned by its maintainers.

### Shipping it: containers, pipelines, and watching it run

Docker lets you package your application together with everything it needs to run (the right Python version, system libraries, etc.) into a single portable unit called a "container" or "image," so it runs the same way regardless of what machine it's deployed to. A "multi-stage" Dockerfile builds the application in one temporary stage (where you might need extra build tools) and then copies only the final, necessary result into a smaller, cleaner final image — keeping the shipped image lean and reducing what could go wrong or be attacked. Running as a "non-root user" inside the container means the application doesn't have full administrative power inside its own container, which limits the damage if it's ever compromised.

CI/CD stands for continuous integration / continuous delivery. In practice, it means: every time someone proposes a code change, an automated pipeline (commonly GitHub Actions) automatically runs your linter, type checker, and tests, so broken code is caught before it's merged, without relying on someone remembering to check manually. "Branch protection" enforces this by refusing to let code be merged until those automated checks pass.

"Observability" is the general idea of being able to understand what's happening inside a running system without having to guess. Structured logging means writing log messages in a consistent, machine-readable format (often JSON) rather than free-form sentences, so logs can be searched and filtered reliably. A "correlation ID" is a unique tag attached to a single request as it flows through multiple parts of a system, so you can later find every log line related to that one specific request, even across different services.

Sentry (or similar tools) automatically captures and reports errors that happen in your running application, often with helpful context, so you find out about problems from your monitoring rather than from a customer complaint. "Tracing" (such as with OpenTelemetry) tracks a single request's journey through multiple steps or services, showing you where time was spent along the way — useful for understanding slow requests that touch many parts of a system.

A "health check" endpoint is a simple URL your application exposes that says "yes, I'm alive and working" (and ideally, "and my database connection is working too"), which other systems (like a container orchestrator) use to decide whether to keep sending traffic to this instance or restart it.

---

## Phase 6: Advanced Topics and Senior Engineering Practices

### Metaprogramming: code that shapes code

Metaprogramming means writing code that manipulates or generates other code's behavior, rather than directly doing the work itself. A "metaclass" is, in simple terms, the thing that creates classes — just as a class is a blueprint for creating objects, a metaclass is a blueprint for creating classes themselves. This sounds abstract because it rarely needs to be touched directly; most Python developers go their whole careers barely using custom metaclasses, which is why the roadmap calls them "rarely warranted." `__init_subclass__` offers a much simpler way to run custom logic whenever a class is subclassed, covering many of the use cases people used to reach for metaclasses for, without the complexity.

A "class decorator" is the same decorator idea from Phase 1, but applied to an entire class instead of a single function — wrapping or modifying the whole class when it's defined.

`exec` and `eval` let you run a string of code as if it were actual Python source, dynamically, while the program is running. This is dangerous in production because if that string ever comes from an untrusted source (like user input), you've effectively given an attacker the ability to run arbitrary code inside your application — which is why it's avoided almost everywhere except very controlled, trusted scenarios.

### More advanced typing ideas

Bounded `TypeVar`s let you say "this generic can be any type, but it must be a subtype of this specific base" — restricting a generic placeholder to a known family of types rather than literally anything.

`ParamSpec` solves a specific annoyance: normally, when you write a decorator, the type checker loses track of exactly what arguments the original wrapped function accepted. `ParamSpec` lets a decorator preserve and pass through that exact argument signature so type checking still works correctly on the decorated function.

"Variance" (covariance and contravariance) is a subtle rule about whether a generic container of a subtype can safely be used where a generic container of the parent type is expected. A simple mental anchor: if you have a list of dogs, is it safe to treat it as a list of animals? For a read-only, you-can-only-take-things-out container, yes. For a container someone could also put new animals into, allowing a non-dog "animal" to be added into what's supposed to be a dog-only list would break things. This rule exists to stop that kind of type-unsafe substitution quietly compiling when it shouldn't.

Type stubs (`.pyi` files) are separate files that describe the types for a library's functions and classes without touching the library's actual source code — useful for adding type information to a third-party package that wasn't written with type hints itself.

### Understanding what's happening under the hood with memory

Python automatically manages memory mostly through "reference counting": every object keeps a running count of how many things are currently pointing at it, and once that count hits zero (nothing references it anymore), Python frees that memory. On top of this, a "garbage collector" exists to clean up more complicated situations — specifically, groups of objects that reference each other in a cycle (A points to B, B points back to A) so their reference counts never naturally reach zero on their own, even though nothing outside the cycle actually needs them anymore.

A "weak reference" lets you point at an object without that pointer counting toward keeping it alive — useful for things like caches, where you want to remember an object if it still exists elsewhere, but you don't want your cache itself to be the reason it never gets cleaned up (which would be a memory leak).

The "mutable default argument" bug is a famous, very common Python gotcha: if you write `def add_item(item, items=[]):`, that empty list is created exactly once, when the function is defined — not freshly each time the function is called. So every call that doesn't pass its own list ends up silently sharing and mutating the *same* list across calls, leading to very confusing bugs. The fix is to default to `None` and create a fresh list inside the function body when needed.

`copy` and `deepcopy` both make a duplicate of an object, but `copy` (shallow copy) only duplicates the outer container — any objects nested inside are still shared with the original. `deepcopy` recursively duplicates everything nested inside too, so the copy is completely independent all the way down. This matters a lot with nested, mutable structures, where a shallow copy can give a false sense of safety.

### What "senior engineering judgment" actually looks like

Good code review isn't just nitpicking formatting — it means genuinely checking whether the logic is correct, whether another engineer could understand and safely modify this code later, and distinguishing between "this is a blocking problem" versus "this is a nice-to-have suggestion," so authors know what actually needs fixing before merging versus what's optional polish.

"Premature abstraction" is building flexible, generic machinery for problems you don't actually have yet, guessing at future needs — which often adds complexity without ever paying off, because the guessed-at future rarely matches what's actually needed later. The skill is telling that apart from genuine, present complexity that really does need a more sophisticated structure right now.

An RFC or design doc is a written explanation of a proposed non-trivial change, written before building it, so other people can question the approach while it's still just an idea — much cheaper to change a sentence in a document than to rewrite already-built code. Documenting trade-offs means explicitly writing down *why* you chose one approach over the alternatives you considered, which is hugely valuable to future readers (including future you) trying to understand whether something can safely be changed.

On security: `pickle` is Python's way of serializing objects (turning them into bytes to store or send, and back again), but unpickling data from an untrupted source is dangerous because a crafted pickle can execute arbitrary code during that process — so it should never be used on data you don't fully trust. SQL injection is when untrusted input gets directly inserted into a SQL query as raw text, letting an attacker manipulate the query itself (for example, to bypass a login check); "parameterized queries" avoid this by keeping user input strictly separated from the query's structure, so it's always treated as plain data, never as part of the command. Secrets (passwords, API keys) should never be hardcoded directly into source code or accidentally written into log files, since both are easy ways for them to leak.

Debugging production issues well means working from evidence rather than guessing: reading a stack trace from the bottom up (the deepest, most specific cause is usually listed first), using logs and traces to narrow down roughly where the problem lives before diving into code, and — critically — writing a test that reproduces the bug *before* fixing it. That way you can prove the fix actually works, and that test keeps protecting you against the same bug sneaking back in later (a "regression").
