---
name: "flutter-building-layouts"
description: "Builds Flutter layouts using the constraint system and layout widgets. Use when creating or refining the UI structure of a Flutter application."
---
# Architecting Flutter Layouts

Core layout rule: **Constraints go down. Sizes go up. Parent sets position.**

Use `Row`/`Column` for linear layouts, `Expanded`/`Flexible` to fill space, `Stack` for overlapping, `SizedBox` for strict constraints. Use `LayoutBuilder` for responsive layouts. Always wrap `ListView` in `Expanded` when inside a `Column`.
