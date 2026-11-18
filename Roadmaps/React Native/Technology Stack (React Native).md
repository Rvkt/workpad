---
tags: [roadmap, roadmap/react-native]
---

# Technology Stack

Part of [[React Native Roadmap - Index|React Native Application — Complete Implementation Roadmap]].

| Category | Technology | Purpose |
|---|---|---|
| Framework | React Native + Expo | Cross-platform application development |
| Language | TypeScript | Static typing and maintainability |
| Navigation | Expo Router | File-based routing and deep linking |
| Client state | Zustand | Shared client-side state |
| Server state | TanStack Query | API caching and asynchronous server state |
| HTTP client | Axios | API requests, timeouts and interceptors |
| Forms | React Hook Form | Form state and submission handling |
| Validation | Zod | Runtime validation and typed schemas |
| Styling | NativeWind or React Native StyleSheet | Shared visual styling |
| UI components | React Native Reusables, where compatible | Reusable interface components |
| Native secure storage | Expo SecureStore | Secure storage of appropriate native credentials |
| Unit testing | Jest / jest-expo | Unit and integration tests |
| Component testing | React Native Testing Library | Component behavior |
| E2E testing | Maestro | Critical user-flow testing |
| Backend | Django REST Framework | REST API |
| Database | PostgreSQL | Persistent relational data |
| API documentation | OpenAPI / Swagger | API contract documentation |
| Monitoring | Deferred | Add after core implementation |
| Build and deployment | Deferred | Add after platform verification |

### Dependency management rules

- Use Expo-compatible versions of React Native native dependencies.
- Prefer `npx expo install` for Expo-compatible native packages.
- Keep one package manager and its lockfile.
- Avoid adding a second state management library without a concrete requirement.
- Reassess NativeWind and UI library compatibility with the selected Expo SDK before adopting them.
