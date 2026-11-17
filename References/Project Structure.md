# Recommended Project Structure

Part of [[Flutter Roadmap - Index|Senior Flutter Developer Roadmap]]. Used in [[Phase 2 - Architecture and Backend Integration]].

Start with a single application repository. Introduce separate Dart packages only when module boundaries and reuse justify them.

```text
lib/
├── app/
│   ├── app.dart
│   ├── router/
│   └── theme/
│
├── core/
│   ├── network/
│   ├── errors/
│   ├── storage/
│   ├── logging/
│   ├── constants/
│   └── design_system/
│
├── features/
│   ├── authentication/
│   │   ├── presentation/
│   │   │   ├── screens/
│   │   │   ├── widgets/
│   │   │   └── providers/
│   │   ├── domain/
│   │   │   ├── entities/
│   │   │   ├── repositories/
│   │   │   └── use_cases/
│   │   └── data/
│   │       ├── models/
│   │       ├── data_sources/
│   │       └── repositories/
│   │
│   └── dashboard/
│       ├── presentation/
│       ├── domain/
│       └── data/
│
└── main.dart
```
