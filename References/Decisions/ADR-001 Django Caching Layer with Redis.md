---
type: decision
status: accepted
created: 2026-10-21
project: "[[Surfari Mobile Client]]"
tags:
  - decision
  - adr
  - django
  - redis
---

# ⚖️ ADR-001: Django Caching Layer with Redis

> [!work] Decision Status: Accepted
> **Deciders:** Ravi Kant
> **Date:** 2026-10-21

---

## 🔍 Context & Problem Statement
The mobile client makes heavy polling requests for live wave data and forecast models. Direct database hits to PostgreSQL on every telemetry request cause severe latency and DB connection exhaustion during peak morning hours.

## 🧭 Options Considered
1. **Option A: PostgreSQL Query Caching & Materialized Views**
   - *Pros:* No new infrastructure service required.
   - *Cons:* Refreshing materialized views is slow; high write lock overhead.
2. **Option B: Distributed Redis Cache with Cache-Aside Pattern**
   - *Pros:* Sub-millisecond reads; atomic expiration (`SETEX`); seamless Django cache backend.
   - *Cons:* Requires managing a Redis instance; cache invalidation complexity.

## 🏆 Decision Outcome
**Chosen Option:** **Option B — Redis Cache with 15-minute TTL & Cache-Aside**
**Justification:** Eliminates 90% of repeat DB queries, supporting thousands of concurrent Flutter clients with sub-50ms API response times.

## 🔗 Related Notes
- Project: [[Surfari Mobile Client|Surfari Mobile Client]]
- Concept: [[Optimistic UI Updates in Flutter|Optimistic UI Updates]]
- Work MOC: [[Work MOC|Work MOC]]
