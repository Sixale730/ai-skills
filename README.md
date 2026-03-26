# ai-skills

Shared AI agent skills — reusable commands, agents, and workflows for AI-assisted development.

## Install

```bash
npx skills add Sixale730/ai-skills@<skill-name> -g -y
```

## Skills

### Flutter & Dart (Official - flutter/skills, 819★)

| Skill | Description |
|-------|-------------|
| `flutter-architecting-apps` | Layered architecture (UI, Logic, Data), SSOT, UDF |
| `flutter-managing-state` | MVVM + Provider, ephemeral vs app state |
| `flutter-building-layouts` | Constraint system, responsive layouts |
| `flutter-implementing-navigation-and-routing` | Navigator, GoRouter, deep linking |
| `flutter-theming-apps` | Material 3, ColorScheme.fromSeed(), adaptive design |

### Flutter & Dart (Community)

| Skill | Source | Description |
|-------|--------|-------------|
| `flutter-expert` | jeffallan/claude-skills (7.3K★) | Full-stack Flutter: Riverpod, Bloc, GoRouter, performance |
| `flutter-architecture` | madteacher/mad-agents-skills (1.2K installs) | MVVM, feature-first, Command/Result patterns |
| `flutter-dart-code-review` | affaan-m/everything-claude-code | 15-category code review checklist |
| `dart-best-practices` | kevmoo/dash_skills (119★, Dart team) | Idiomatic Dart style and usage |
| `dart-test-fundamentals` | kevmoo/dash_skills (119★, Dart team) | package:test, groups, lifecycle, config |

### Backend & Database

| Skill | Source | Description |
|-------|--------|-------------|
| `supabase-postgres-best-practices` | supabase/agent-skills (1.7K★) | 8 categories: query, conn, security, schema, locking, data, monitoring |

### Code Quality & Security

| Skill | Source | Description |
|-------|--------|-------------|
| `code-review-quality` | proffesor-for-testing/agentic-qe (745 installs) | Context-driven code reviews with severity levels |
| `security-auditor` | ovachiever/droid-tings (513 installs) | OWASP Top 10 vulnerability scanning |

### Utilities

| Skill | Description |
|-------|-------------|
| `find-skills` | Multi-source skill discovery (skills.sh, GitHub, Context7, web, package managers) |

## Structure

```
skills/           → Agent skills (SKILL.md + optional references/)
commands/         → Slash commands (invoked with /command-name)
```

## Contributing

Each skill should:
1. Have clear frontmatter (`name`, `description`)
2. Include step-by-step protocol
3. Define when to use AND when NOT to use
4. List anti-patterns to avoid
