---
tags: [roadmap, roadmap/react-native]
---

# Phase 3 — Navigation and Application Shell

Part of [[React Native Roadmap - Index|React Native Application — Complete Implementation Roadmap]]. Previous: [[Phase 2 - TypeScript, Code Quality and Project Structure]]. Next: [[Phase 4 - UI Foundation and Design System]].

**Objective:** Establish navigation and shared application layouts.

### Tasks

- Configure Expo Router.
- Create root layout.
- Add authentication and application route groups.
- Create the initial landing screen.
- Create a shared screen container.
- Implement responsive layouts for mobile and web.
- Add a not-found route.
- Define route parameter conventions.
- Verify deep links and browser refresh behavior.
- Handle the web back and forward buttons correctly.

### Navigation principles

- Use route groups to organize application sections.
- Use route parameters for shareable, navigable resource identifiers.
- Avoid duplicating navigation state in Zustand when Expo Router already owns it.
- Protect authenticated routes through a consistent session-aware navigation strategy.

### Exit criteria

- Navigation works on Android, iOS, and web.
- Direct web URLs work as expected.
- Authentication and application routes are separated.
- Back navigation is predictable.

**Deliverable:** A functional application shell.
