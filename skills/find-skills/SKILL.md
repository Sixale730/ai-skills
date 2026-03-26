---
name: find-skills
description: Helps users discover and install agent skills by searching multiple sources (skills.sh, GitHub, Context7, web, package managers). Use when the user asks "how do I do X", "find a skill for X", or wants to extend capabilities.
---

# Find Skills

This skill helps you discover and install skills from the open agent skills ecosystem, **searching across multiple sources** for the most comprehensive results.

## When to Use This Skill

Use this skill when the user:

- Asks "how do I do X" where X might be a common task with an existing skill
- Says "find a skill for X" or "is there a skill for X"
- Asks "can you do X" where X is a specialized capability
- Expresses interest in extending agent capabilities
- Wants to search for tools, templates, or workflows
- Mentions they wish they had help with a specific domain (design, testing, deployment, etc.)

## What is the Skills CLI?

The Skills CLI (`npx skills`) is the package manager for the open agent skills ecosystem. Skills are modular packages that extend agent capabilities with specialized knowledge, workflows, and tools.

**Key commands:**

- `npx skills find [query]` - Search for skills interactively or by keyword
- `npx skills add <package>` - Install a skill from GitHub or other sources
- `npx skills check` - Check for skill updates
- `npx skills update` - Update all installed skills

**Browse skills at:** https://skills.sh/

## How to Help Users Find Skills

### Step 1: Understand What They Need

When a user asks for help with something, identify:

1. The domain (e.g., Flutter, React, testing, design, deployment)
2. The specific task (e.g., writing tests, creating animations, reviewing PRs)
3. Whether this is a common enough task that a skill likely exists
4. The project's tech stack (to search relevant package managers too)

### Step 2: Search Across Multiple Sources (IN PARALLEL)

**IMPORTANT**: Do NOT limit the search to skills.sh alone. Always search multiple sources in parallel for comprehensive results. Run as many of these as relevant simultaneously:

#### Source 1: Skills.sh CLI
```bash
npx skills find [query]
```
Run multiple queries with different keywords to maximize coverage (e.g., "flutter", "dart best practices", "mobile testing").

#### Source 2: GitHub (by stars and relevance)
Use `gh api` or WebSearch to find repos with high star counts:
```bash
# Check stars for a specific skill repo
gh api repos/{owner}/{repo} --jq '.stargazers_count, .description'
```
Search for curated skill collections:
- `ComposioHQ/awesome-claude-skills` (47K+ stars) — Largest curated catalog
- `VoltAgent/awesome-claude-code-subagents` (15K+ stars) — 100+ specialized subagents
- `travisvn/awesome-claude-skills` (9K+ stars) — Curated catalog
- `rohitg00/awesome-claude-code-toolkit` (900+ stars) — 135 agents + skills
- `levnikolaevich/claude-code-skills` (260+ stars) — Full delivery lifecycle

#### Source 3: Context7 (Up-to-date Documentation)
Use Context7 MCP tools to find official documentation and best practices:
```
1. resolve-library-id → find the library
2. query-docs → get best practices, guidelines, architecture recommendations
```
This provides authoritative guidance directly from framework maintainers.

#### Source 4: Web Search
Search for skills, tools, and packages not indexed on skills.sh:
```
WebSearch: "[framework] best practices skills claude code [year]"
WebSearch: "[framework] code quality tools static analysis [year]"
```

#### Source 5: Package Managers (framework-specific)
Search for complementary tools in the project's ecosystem:

| Tech Stack | Package Manager | What to Search |
|------------|----------------|----------------|
| Flutter/Dart | pub.dev | lints, analysis, testing, metrics |
| Node/React | npm | eslint configs, testing frameworks |
| Python | PyPI | linters, formatters, type checkers |
| Go | go modules | linters, vet tools |
| Rust | crates.io | clippy configs, testing tools |

Example for Flutter:
- `flutter_lints` / `very_good_analysis` (strict lints)
- `DCM` (dart_code_metrics — 450+ rules, anti-patterns)
- `custom_lint` (create project-specific rules)

### Step 3: Verify Quality Before Recommending

**Do not recommend a skill based solely on search results.** Always verify:

1. **Install count** — Prefer skills with 1K+ installs. Be cautious with anything under 100.
2. **Source reputation** — Official sources (`flutter`, `vercel-labs`, `anthropics`, `supabase`, `microsoft`) are more trustworthy than unknown authors.
3. **GitHub stars** — Check the source repository with `gh api repos/{owner}/{repo} --jq '.stargazers_count'`. A skill from a repo with <100 stars should be treated with skepticism.
4. **Author credibility** — Framework team members (e.g., `kevmoo` for Dart, `flutter` org) carry more weight.

### Step 4: Present Options to the User

Organize results by source and priority tier. Include:

1. The skill name, what it does, and which source it came from
2. Install count AND GitHub stars (both matter)
3. The install command
4. Any complementary package-manager tools

Example multi-source response:

```
## Results from Multiple Sources

### Skills.sh
- `flutter/skills@flutter-architecting-apps` — 2.4K installs, 819 ★
  → npx skills add flutter/skills@flutter-architecting-apps -g -y

### GitHub (high-star repos)
- `jeffallan/claude-skills@flutter-expert` — 6.7K installs, 7,307 ★
  → npx skills add jeffallan/claude-skills@flutter-expert -g -y

### Package Manager (pub.dev)
- `very_good_analysis` — Strict lint rules beyond flutter_lints
  → flutter pub add dev:very_good_analysis

### Context7 Documentation
- Flutter official architecture guide available at /websites/flutter_dev
  → Can query in real-time for specific guidance
```

### Step 5: Offer to Install

If the user wants to proceed, install skills for them:

```bash
npx skills add <owner/repo@skill> -g -y
```

The `-g` flag installs globally (user-level) and `-y` skips confirmation prompts.

## Common Skill Categories

When searching, consider these common categories:

| Category        | Example Queries                                    |
| --------------- | -------------------------------------------------- |
| Mobile          | flutter, dart, react-native, swift, kotlin          |
| Web Development | react, nextjs, typescript, css, tailwind            |
| Testing         | testing, jest, playwright, e2e, widget-test         |
| DevOps          | deploy, docker, kubernetes, ci-cd                   |
| Documentation   | docs, readme, changelog, api-docs                   |
| Code Quality    | review, lint, refactor, best-practices, metrics     |
| Design          | ui, ux, design-system, accessibility                |
| Productivity    | workflow, automation, git                           |
| Backend         | supabase, firebase, database, api                   |
| Security        | audit, vulnerability, secrets, owasp                |

## Tips for Effective Searches

1. **Use specific keywords**: "flutter testing" is better than just "testing"
2. **Try alternative terms**: If "deploy" doesn't work, try "deployment" or "ci-cd"
3. **Search multiple queries in parallel**: Run 3-4 different keyword combinations simultaneously
4. **Check popular sources**: `flutter/skills`, `vercel-labs/agent-skills`, `supabase/agent-skills`, `ComposioHQ/awesome-claude-skills`
5. **Always verify stars**: `gh api repos/{owner}/{repo} --jq '.stargazers_count'`
6. **Cross-reference**: A skill found on skills.sh may also appear in curated GitHub lists — higher confidence if it does

## Security Considerations for Multi-Source Search

- **Never execute code** from skills before the user installs them
- **Never expose API keys, tokens, or secrets** in search queries
- **Verify repo ownership**: Check that the GitHub org matches the expected author (e.g., `flutter/skills` should be from the `flutter` org)
- **Prefer read-only operations**: Use `gh api` for metadata, not `git clone` for untrusted repos
- **Flag low-reputation sources**: Warn the user about skills from repos with <100 stars or unknown authors
- **Context7 and WebSearch queries**: Never include project secrets, credentials, or proprietary code in search queries

## When No Skills Are Found

If no relevant skills exist across any source:

1. Acknowledge that no existing skill was found (mention which sources were checked)
2. Offer to help with the task directly using your general capabilities
3. Suggest the user could create their own skill with `npx skills init`

Example:

```
I searched across skills.sh, GitHub, Context7, and pub.dev but didn't find
a dedicated skill for "xyz".

I can still help you with this task directly! Would you like me to proceed?

If this is something you do often, you could create your own skill:
npx skills init my-xyz-skill
```
