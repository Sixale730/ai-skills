---
name: dart-test-fundamentals
description: |-
  Core concepts and best practices for `package:test`.
  Covers `test`, `group`, lifecycle methods (`setUp`, `tearDown`), and configuration (`dart_test.yaml`).
license: Apache-2.0
---

# Dart Test Fundamentals

## When to use this skill
Use this skill when:
- Writing new test files.
- Structuring test suites with `group`.
- Configuring test execution via `dart_test.yaml`.
- Understanding test lifecycle methods.

## Core Concepts

### Test Structure (`test` and `group`)
- **`test`**: The fundamental unit of testing.
- **`group`**: Organize tests into logical blocks. Groups can be nested.
- **Naming**: Use `PascalCase` for groups that correspond to a class name. Avoid redundant "test" prefixes.

### Lifecycle Methods
- **`setUp`**: Runs before every `test` in the current `group`.
- **`tearDown`**: Runs after every `test` in the current `group`.
- **`setUpAll`**: Runs once before any test in the group.
- **`tearDownAll`**: Runs once after all tests in the group.

### Configuration (`dart_test.yaml`)
Platforms, tags, and timeouts.

### File Naming
Test files must end in `_test.dart`. Place tests in the `test/` directory.

## Common commands
- `dart test`: Run all tests.
- `dart test test/path/to/file_test.dart`: Run a specific file.
- `dart test --name "substring"`: Run tests matching a description.
