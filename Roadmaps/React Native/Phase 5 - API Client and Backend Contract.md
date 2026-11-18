---
tags: [roadmap, roadmap/react-native]
---

# Phase 5 — API Client and Backend Contract

Part of [[React Native Roadmap - Index|React Native Application — Complete Implementation Roadmap]]. Previous: [[Phase 4 - UI Foundation and Design System]]. Next: [[Phase 6 - State Management (React Native)]].

**Objective:** Centralize communication with Django REST Framework.

### Tasks

- Define development API configuration.
- Configure environment-specific API base URLs.
- Create a shared Axios instance.
- Set request timeouts.
- Define request and response types.
- Normalize API errors.
- Handle HTTP status codes consistently.
- Support request cancellation where appropriate.
- Define API endpoint conventions.
- Document authentication and pagination contracts.
- Test successful responses and failure scenarios.

### Suggested files

```
src/services/api/
├── api-client.ts
├── api-errors.ts
├── endpoints.ts
└── types.ts
```

### Example API client

```
import axios from 'axios';

export const apiClient = axios.create({
  baseURL: process.env.EXPO_PUBLIC_API_URL,
  timeout: 15_000,
});
```

This is the starting point, not a complete production client. Add authentication handling, response normalization, and environment validation in later steps.

### Backend considerations

- Use consistent error response formats.
- Define pagination and filtering behavior.
- Enforce permissions and authorization on the server.
- Configure CORS for web origins.
- Do not treat frontend validation as a security boundary.
- Never embed secrets in `EXPO_PUBLIC_*` variables.

### Exit criteria

- API configuration works on all target platforms.
- Timeouts and network errors are handled.
- Backend validation errors can be represented consistently.
- API communication is independent of UI components.

**Deliverable:** A reusable API infrastructure layer.
