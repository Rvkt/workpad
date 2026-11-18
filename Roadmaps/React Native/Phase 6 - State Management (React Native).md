---
tags: [roadmap, roadmap/react-native]
---

# Phase 6 — State Management

Part of [[React Native Roadmap - Index|React Native Application — Complete Implementation Roadmap]]. Previous: [[Phase 5 - API Client and Backend Contract]]. Next: [[Phase 7 - Authentication and Session Lifecycle]].

**Objective:** Define clear ownership of server and client state.

### Tasks

- Install Zustand.
- Install TanStack Query.
- Create a shared QueryClient.
- Add QueryClientProvider to the root application layout.
- Establish query key conventions.
- Establish query and mutation hook conventions.
- Define cache freshness defaults.
- Define retry behavior.
- Define mutation invalidation conventions.
- Create Zustand stores only for shared client state.
- Verify components subscribe to the smallest state slices they need.

### State ownership

| State | Owner |
|---|---|
| API responses | TanStack Query |
| API loading and error state | TanStack Query |
| Server data cache | TanStack Query |
| Shared UI preferences | Zustand |
| Selected client-side workspace | Zustand |
| Modal visibility | Local React state |
| Form values and validation | React Hook Form |
| Current route and navigation state | Expo Router |
| Sensitive native credentials | Secure storage strategy |

### Query key conventions

Use structured query keys:

```
export const userKeys = {
  all: ['users'] as const,
  lists: () => [...userKeys.all, 'list'] as const,
  detail: (id: string) =>
    [...userKeys.all, 'detail', id] as const,
};
```

### Rules

- Do not duplicate API responses in Zustand.
- Avoid global state for values used by only one component.
- Keep query keys stable and predictable.
- Invalidate affected queries after successful mutations.
- Clear user-specific cached data when the authenticated account changes.
- Do not persist the entire query cache without a clear requirement.

### Exit criteria

- QueryClient is configured once at the application root.
- Server state and client state have separate ownership.
- Query keys are consistent.
- Cache invalidation works after mutations.

**Deliverable:** A predictable state management foundation.
