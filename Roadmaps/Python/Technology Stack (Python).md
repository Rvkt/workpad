---
tags: [roadmap, roadmap/python]
---

# Recommended Technology Stack

Part of [[Python Roadmap - Index|Senior Python Developer Roadmap]].

## Core Development

- [ ] CPython (latest stable)
- [ ] pyenv or uv for interpreter version management
- [ ] venv / virtualenv
- [ ] VS Code or PyCharm

## Dependency and Package Management

- [ ] uv or Poetry
- [ ] pip-tools (as a lighter-weight alternative)
- [ ] pyproject.toml as the single source of project metadata

## Typing

- [ ] mypy or pyright
- [ ] typing / typing_extensions
- [ ] Pydantic for runtime-validated models

## Testing

- [ ] pytest
- [ ] pytest-cov
- [ ] pytest-asyncio
- [ ] Hypothesis for property-based testing
- [ ] unittest.mock / pytest-mock

## Code Quality and Formatting

- [ ] Ruff (lint + format)
- [ ] Black (if not using Ruff's formatter)
- [ ] pre-commit

## Concurrency and Performance

- [ ] asyncio
- [ ] concurrent.futures
- [ ] multiprocessing
- [ ] cProfile / py-spy
- [ ] memory_profiler

## Web and API Frameworks

- [ ] FastAPI
- [ ] Django / Django REST Framework (where applicable)
- [ ] Uvicorn / Gunicorn

## Data Access

- [ ] SQLAlchemy
- [ ] Alembic for migrations
- [ ] psycopg / asyncpg

## Packaging and Distribution

- [ ] build
- [ ] twine
- [ ] Hatchling or setuptools as the build backend

## Deployment and Observability

- [ ] Docker
- [ ] GitHub Actions
- [ ] structlog / standard logging
- [ ] Sentry
- [ ] OpenTelemetry
