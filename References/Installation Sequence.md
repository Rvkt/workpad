# Recommended Installation Sequence

Part of [[React Native Roadmap - Index|React Native Application — Complete Implementation Roadmap]].

Install only the packages required for the current implementation phase.

### Initial project

```
npx create-expo-app@latest my-app
cd my-app
npx expo start
```

### API and state management

```
npm install zustand @tanstack/react-query axios
```

### Forms and validation

```
npm install react-hook-form zod @hookform/resolvers
```

### Secure native storage

```
npx expo install expo-secure-store
```

### Testing

Follow the current Expo testing setup for `jest-expo` and React Native Testing Library. Install compatible versions after confirming the selected Expo SDK's requirements.

### Styling

Choose one primary styling strategy before building the design system:

- NativeWind for utility-based styling.
- React Native StyleSheet for built-in styling with fewer dependencies.

Do not adopt both as competing styling systems without a clear reason.
