---
allowed-tools: Bash, Read, Glob, WebFetch
argument-hint: [search query]
description: Search and install agent skills from the open skills ecosystem (skills.sh)
---

# Find Skills

Search for agent skills that match the user's needs.

## Instructions

1. If the user provided a query via `$ARGUMENTS`, use it. Otherwise, ask what they need.
2. Run `npx skills find $ARGUMENTS` to search for matching skills.
3. Present the results with: skill name, description, install count, and source.
4. Prefer skills with 1K+ installs from reputable sources (vercel-labs, anthropics, microsoft).
5. If the user wants to install, run: `npx skills add <owner/repo@skill> -g -y`

## Quick Reference

- `npx skills find [query]` — Search skills
- `npx skills add <package> -g -y` — Install a skill
- `npx skills check` — Check for updates
- `npx skills update` — Update all skills
- Browse: https://skills.sh/
