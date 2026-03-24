# ai-skills

Shared AI agent skills — reusable commands, agents, and workflows for AI-assisted development.

## Structure

```
commands/       → Slash commands (invoked with /command-name)
agents/          → Agent subtypes (used as subagent_type)
```

## Skills

| Skill | Type | Description |
|-------|------|-------------|
| `/agent-team` | command | Coordinated agent team orchestration with TeamCreate, design approval before spawning |

## Usage

Copy the files you need into your project's `.claude/` directory:

```bash
# Copy a command to your project
cp commands/agent-team.md /path/to/your-repo/.claude/commands/

# Or copy to your global Claude config (available in all projects)
cp commands/agent-team.md ~/.claude/commands/
```

## Contributing

Each skill should:
1. Have clear frontmatter (`allowed-tools`, `description`)
2. Include step-by-step protocol
3. Define when to use AND when NOT to use
4. List anti-patterns to avoid
