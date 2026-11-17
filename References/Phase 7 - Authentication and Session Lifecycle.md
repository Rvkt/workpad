# Phase 7 — Authentication and Session Lifecycle

Part of [[React Native Roadmap - Index|React Native Application — Complete Implementation Roadmap]]. Previous: [[Phase 6 - State Management (React Native)]]. Next: [[Phase 8 - Forms and Validation]].

**Objective:** Implement authentication without exposing credentials or trusting client-side authorization.

### Tasks

- Define the backend authentication contract.
- Implement login.
- Implement registration if required.
- Implement logout.
- Implement session restoration.
- Define access-token and refresh-token handling.
- Store native credentials using an appropriate secure storage mechanism.
- Design a secure web session strategy.
- Handle expired access tokens.
- Prevent concurrent refresh requests from racing.
- Handle refresh failure.
- Clear account-specific query caches on logout.
- Clear user-specific Zustand state when necessary.
- Implement protected routes.
- Handle network failure during session restoration.

### Security requirements

- Keep access tokens short-lived where appropriate.
- Rotate refresh tokens if supported by the authentication architecture.
- Never log tokens or credentials.
- Never rely on hidden routes as authorization.
- Enforce authorization on the backend.
- Prefer secure, HttpOnly cookies for browser sessions where the backend architecture supports them.
- Do not assume native secure storage provides equivalent security guarantees on the web.

### Exit criteria

- Login and logout work correctly.
- Session restoration is predictable.
- Expired sessions are handled.
- Logout clears account-specific client data.
- Protected screens cannot expose another user's data.
- Authentication behavior is verified on Android, iOS, and web.

**Deliverable:** A complete authentication lifecycle.
