---
type: concept
created: 2026-10-21
status: evergreen
tags:
  - concept
  - flutter
  - architecture
---

# 🧠 Optimistic UI Updates in Flutter

> [!knowledge] One-Sentence Definition
> Updating client UI state immediately upon user interaction before receiving server acknowledgment, with automated rollback on network rejection.

---

## ⚙️ How It Works (Core Mechanics)
1. **User Action:** User favorites a surf spot or changes preferences.
2. **Immediate Local Mutation:** StateNotifier or BLoC emits optimistic `Loaded(isFavorite: true)`.
3. **Async Dispatch:** Repository dispatches `PATCH /api/v1/favorites/` to Django REST API.
4. **Resolution:**
   - **Success:** Retain state quietly.
   - **Failure:** Revert local state and display a non-blocking toast/snackbar notification.

```text
[User Tap] ---> [Local UI State Updates] (Instant 0ms)
                     |
                     v
             [Async REST Dispatch]
                     |
            +--------+--------+
            |                 |
        [Success]          [Error] ---> [Rollback + Toast]
```

## ⚖️ Trade-offs & Considerations
- **Advantages:** Perceived zero-latency user experience; feels native and fluid.
- **Constraints:** Requires deterministic rollback logic and idempotent REST API endpoints.

## 🔗 Connected Notes
- Applied In Project: [[Surfari Mobile Client|Surfari Mobile Client]]
- Architecture Decision: [[ADR-001 Django Caching Layer with Redis|ADR-001 Django Caching Layer with Redis]]
- Map of Content: [[Knowledge MOC|Knowledge MOC]]
