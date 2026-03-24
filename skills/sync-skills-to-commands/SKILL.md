---
name: sync-skills-to-commands
description: Scans installed skills in .claude/skills/ and ~/.claude/skills/, reads their SKILL.md metadata, and generates matching slash commands in .claude/commands/ so every skill is invocable via /skill-name.
---

# Sync Skills to Commands

Automatically generate slash commands (`.claude/commands/*.md`) for every installed skill that doesn't already have one.

## When to Use

- After installing new skills with `npx skills add`
- When the user says "sync skills", "register skills", or "make skills available as commands"
- Periodically to keep commands in sync with installed skills

## How It Works

### Step 1: Discover installed skills

Scan both locations for skill directories containing a `SKILL.md`:

```
.claude/skills/*/SKILL.md          (project-level)
~/.claude/skills/*/SKILL.md        (global/user-level)
```

### Step 2: Parse each SKILL.md

Extract from the YAML frontmatter:
- `name` — the skill name (used as command filename)
- `description` — short description (used in command frontmatter)
- `allowed-tools` — if present, pass through to the command
- `argument-hint` — if present, pass through to the command

Also check if the skill has `disable-model-invocation: true` or `user-invocable: false` — if so, **skip it** (these are background/passive skills not meant for direct invocation).

### Step 3: Check for existing commands

For each skill, check if `.claude/commands/{skill-name}.md` already exists.
- If it exists → **skip** (don't overwrite user customizations)
- If it doesn't exist → **generate** a new command file

### Step 4: Generate the command file

Create `.claude/commands/{skill-name}.md` with this template:

```markdown
---
allowed-tools: {from SKILL.md or default: Bash, Read, Write, Edit, Glob, Grep}
argument-hint: {from SKILL.md or "[arguments]"}
description: {from SKILL.md description}
---

# {skill name}

{first paragraph of SKILL.md body as context}

ARGUMENTS: $ARGUMENTS
```

### Step 5: Report results

Output a summary table:

| Skill | Status |
|-------|--------|
| find-skills | Created /find-skills |
| self-improvement-ci | Skipped (already exists) |
| generate_command | Created /generate_command |

## Rules

- **Never overwrite** existing command files — user customizations take priority
- **Skip** skills with `user-invocable: false` or `disable-model-invocation: true`
- **Skip** skills whose SKILL.md has no `description` field
- Command filenames should match the skill directory name exactly
- Use the skill's `allowed-tools` if specified, otherwise default to `Bash, Read, Write, Edit, Glob, Grep`
- Always include `$ARGUMENTS` pass-through so users can pass arguments to the command

## Example

Given a skill at `.claude/skills/find-skills/SKILL.md`:

```yaml
---
name: find-skills
description: Helps users discover and install agent skills
---
```

Generates `.claude/commands/find-skills.md`:

```markdown
---
allowed-tools: Bash, Read, Glob, WebFetch
description: Helps users discover and install agent skills
argument-hint: [search query]
---

# find-skills

Helps users discover and install agent skills from the open skills ecosystem.

ARGUMENTS: $ARGUMENTS
```
