---
tags: [roadmap, roadmap/react-native]
---

# Phase 11 — Cross-Platform Verification

Part of [[React Native Roadmap - Index|React Native Application — Complete Implementation Roadmap]]. Previous: [[Phase 10 - Testing (React Native)]]. Next: [[Phase 12 - Release Preparation Without Deployment Automation]].

**Objective:** Identify behavior that differs across Android, iOS, and web.

### Android

- Verify permissions.
- Verify keyboard and back-button behavior.
- Verify deep links.
- Verify network connectivity and API configuration.
- Verify secure storage.
- Verify screen-size and orientation behavior where supported.

### iOS

- Verify permissions and native prompts.
- Verify keyboard and navigation behavior.
- Verify deep links.
- Verify secure storage.
- Verify safe areas and device-specific layouts.

### Web

- Verify browser refresh.
- Verify direct navigation to nested routes.
- Verify browser back and forward navigation.
- Verify responsive layouts.
- Verify session security.
- Verify CORS and API configuration.
- Verify keyboard accessibility and focus behavior.

### Exit criteria

- Critical user flows work across supported platforms.
- Platform-specific limitations are documented.
- No known critical defects remain.

**Deliverable:** A cross-platform verified application.
