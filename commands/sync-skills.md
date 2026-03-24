---
allowed-tools: Bash, Read, Write, Glob, Grep
description: Scan installed skills and generate slash commands for each one
---

# Sync Skills to Commands

Scan all installed skills and create slash commands for any that don't have one yet.

## Instructions

1. **Find all installed skills** by scanning:
   - `.claude/skills/*/SKILL.md` (project-level)
   - `~/.claude/skills/*/SKILL.md` (global-level)

2. **For each skill**, read its `SKILL.md` frontmatter to extract: `name`, `description`, `allowed-tools`, `argument-hint`.

3. **Skip** if:
   - `.claude/commands/{skill-name}.md` already exists
   - The skill has `user-invocable: false` or `disable-model-invocation: true`
   - No `description` in frontmatter

4. **Generate** `.claude/commands/{skill-name}.md` with:
   ```
   ---
   allowed-tools: {from skill or default: Bash, Read, Write, Edit, Glob, Grep}
   argument-hint: {from skill or "[arguments]"}
   description: {from skill description}
   ---

   # {skill name}

   {first paragraph of SKILL.md body}

   ARGUMENTS: $ARGUMENTS
   ```

5. **Report** a summary table of what was created vs skipped.
