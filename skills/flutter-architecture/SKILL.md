---
name: flutter-architecture
description: Comprehensive guide for architecting Flutter applications following MVVM pattern and best practices with feature-first project organization.
metadata:
  author: Stanislav [MADTeacher] Chernyshev
  version: "1.0"
---

# Flutter Architecture

MVVM pattern, layered architecture (UI, Data, Domain), feature-first project organization.

## Project Structure: Feature-First vs Layer-First

Feature-first recommended for teams (10+ features, 2+ devs). Layer-first for small apps.

## Core Components
- **Views**: Compose widgets, minimal logic
- **ViewModels**: Transform repo data into UI state, ChangeNotifier
- **Repositories**: SSOT, aggregate from services, caching
- **Services**: Wrap external data sources, stateless

## Design Patterns
- Command Pattern (encapsulate actions with Result handling)
- Result Type (type-safe error handling)
- Repository Pattern (abstraction over data sources)
- Offline-First (optimistic UI updates with sync)

## References
- references/concepts.md - Core architectural principles
- references/feature-first.md - Feature-first organization
- references/mvvm.md - MVVM implementation
- references/layers.md - Layer responsibilities
- references/design-patterns.md - Common patterns
- assets/command.dart - Command pattern template
- assets/result.dart - Result type implementation
