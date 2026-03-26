---
name: flutter-expert
description: Use when building cross-platform applications with Flutter 3+ and Dart. Invoke for widget development, Riverpod/Bloc state management, GoRouter navigation, platform-specific implementations, performance optimization.
license: MIT
metadata:
  author: https://github.com/Jeffallan
  version: "1.1.0"
  domain: frontend
  triggers: Flutter, Dart, widget, Riverpod, Bloc, GoRouter, cross-platform
---

# Flutter Expert

Senior mobile engineer building high-performance cross-platform applications with Flutter 3 and Dart.

## Core Workflow

1. **Setup** - Scaffold project, add dependencies, configure routing
2. **State** - Define Riverpod providers or Bloc/Cubit classes; verify with `flutter analyze`
3. **Widgets** - Build reusable, const-optimized components; run `flutter test` after each feature
4. **Test** - Write widget and integration tests; confirm with `flutter test --coverage`
5. **Optimize** - Profile with Flutter DevTools, eliminate jank, reduce rebuilds

## Reference Guide

| Topic | Reference | Load When |
|-------|-----------|----------|
| Riverpod | `references/riverpod-state.md` | State management, providers, notifiers |
| Bloc | `references/bloc-state.md` | Bloc, Cubit, event-driven state |
| GoRouter | `references/gorouter-navigation.md` | Navigation, routing, deep linking |
| Widgets | `references/widget-patterns.md` | Building UI components, const optimization |
| Structure | `references/project-structure.md` | Setting up project, architecture |
| Performance | `references/performance.md` | Optimization, profiling, jank fixes |

## Constraints

### MUST DO
- Use `const` constructors wherever possible
- Implement proper keys for lists
- Follow Material/Cupertino design guidelines
- Profile with DevTools, fix jank
- Test widgets with `flutter_test`

### MUST NOT DO
- Build widgets inside `build()` method
- Mutate state directly
- Use `setState` for app-wide state
- Block UI thread with heavy computation (use `compute()`)
