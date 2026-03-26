---
name: flutter-dart-code-review
description: Library-agnostic Flutter/Dart code review checklist covering widget best practices, state management patterns (BLoC, Riverpod, Provider, GetX, MobX, Signals), Dart idioms, performance, accessibility, security, and clean architecture.
origin: ECC
---

# Flutter/Dart Code Review Best Practices

Comprehensive, library-agnostic checklist for reviewing Flutter/Dart applications. Covers:

1. **General Project Health** - folder structure, separation of concerns, pubspec, analysis_options
2. **Dart Language Pitfalls** - implicit dynamic, null safety, type promotion, catching errors
3. **Widget Best Practices** - decomposition, const usage, key usage, theming, build complexity
4. **State Management** - architecture, immutability, reactivity, rebuild optimization, disposal
5. **Performance** - unnecessary rebuilds, expensive build ops, image optimization, lazy loading
6. **Testing** - unit, widget, integration, golden tests, coverage targets
7. **Accessibility** - semantic widgets, screen reader, visual, interaction
8. **Platform-Specific** - iOS/Android differences, responsive design
9. **Security** - secure storage, API keys, input validation, network security
10. **Package/Dependency Review** - pub.dev evaluation, version constraints
11. **Navigation and Routing** - consistency, typed arguments, auth guards
12. **Error Handling** - FlutterError.onError, error reporting, graceful degradation
13. **Internationalization** - l10n setup, ICU syntax, locale-aware formatting
14. **Dependency Injection** - abstractions, lifetime, environment bindings
15. **Static Analysis** - analysis_options.yaml, strict settings, CI enforcement

Includes State Management Quick Reference table for BLoC, Riverpod, Provider, GetX, MobX, Signals, and Built-in.
