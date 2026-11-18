---
tags: [roadmap, roadmap/react-native]
---

# Phase 2 — TypeScript, Code Quality and Project Structure

Part of [[React Native Roadmap - Index|React Native Application — Complete Implementation Roadmap]]. Previous: [[Phase 1 - Project Initialization]]. Next: [[Phase 3 - Navigation and Application Shell]].

**Objective:** Establish consistent code organization before feature development.

### Tasks

- Enable TypeScript strict mode.
- Configure import aliases.
- Establish ESLint rules.
- Configure code formatting.
- Define file naming conventions.
- Separate screens, features, services, stores, and shared components.
- Establish rules for exports and module dependencies.
- Add a minimal README documenting local development.

### Recommended structure

```
my-app/
├── app/
│   ├── _layout.tsx
│   ├── index.tsx
│   ├── (auth)/
│   │   ├── _layout.tsx
│   │   ├── login.tsx
│   │   └── register.tsx
│   └── (app)/
│       ├── _layout.tsx
│       └── dashboard.tsx
├── src/
│   ├── components/
│   │   ├── ui/
│   │   └── feedback/
│   ├── features/
│   │   ├── auth/
│   │   └── dashboard/
│   ├── services/
│   │   └── api/
│   │       ├── api-client.ts
│   │       ├── api-errors.ts
│   │       └── endpoints.ts
│   ├── queries/
│   │   ├── auth/
│   │   └── dashboard/
│   ├── stores/
│   │   └── app.store.ts
│   ├── providers/
│   │   └── query-provider.tsx
│   ├── schemas/
│   ├── hooks/
│   ├── types/
│   ├── constants/
│   └── utils/
├── assets/
├── app.json
├── package.json
├── tsconfig.json
└── README.md
```

### Conventions

- Use `app/` for route definitions and route layouts.
- Use `src/features/` for feature-specific UI and logic.
- Use `src/services/` for infrastructure such as HTTP communication.
- Use `src/queries/` for reusable query and mutation hooks.
- Use `src/stores/` for Zustand stores.
- Avoid creating abstractions that have only one trivial use without a clear reason.

### Exit criteria

- TypeScript strict mode passes.
- Imports resolve consistently.
- Linting and formatting work.
- Directory responsibilities are documented.

**Deliverable:** A predictable codebase ready for implementation.
