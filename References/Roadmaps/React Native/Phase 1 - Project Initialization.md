# Phase 1 — Project Initialization

Part of [[React Native Roadmap - Index|React Native Application — Complete Implementation Roadmap]]. Next: [[Phase 2 - TypeScript, Code Quality and Project Structure]].

**Objective:** Create a working cross-platform development environment.

### Tasks

- Install Node.js LTS.
- Install Android Studio and the Android SDK.
- Configure Android SDK environment variables.
- Install Expo-compatible development tooling.
- Create the Expo TypeScript project.
- Verify the app starts on Android.
- Verify the app starts on web.
- Verify the iOS workflow using macOS/Xcode or a supported device workflow.
- Confirm the project's package manager and lockfile.
- Initialize Git and establish a `.gitignore`.

### Commands

```
npx create-expo-app@latest my-app
cd my-app
npx expo start
```

Platform-specific development:

```
npx expo start --android
npx expo start --web
npx expo start --ios
```

The iOS simulator requires macOS and Xcode. Windows developers can use a physical iOS device through a compatible workflow or a supported cloud build.

### Exit criteria

- Application starts successfully.
- No unresolved dependency or SDK errors.
- Android and web are verified.
- iOS workflow is documented and verified where available.

**Deliverable:** A clean, working Expo application.
