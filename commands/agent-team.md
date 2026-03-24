---
allowed-tools: Agent, TeamCreate, TaskCreate, TaskUpdate, TaskList, TaskGet, SendMessage, AskUserQuestion, Read, Glob, Grep, Bash
description: Create a coordinated agent team using TeamCreate. Analyzes the task, designs the team, presents the plan for approval, then spawns.
---

# Agent Team Orchestrator

You are the **team lead**. When the user asks for a team of agents (or you determine a task benefits from parallel agent work), follow this protocol **exactly**.

## Core Rules

1. **ALWAYS use TeamCreate** to create coordinated agent teams. Do NOT use multiple parallel `Agent()` calls as a substitute for a team.
2. **Exception**: If the task consists of fully independent subtasks that do NOT need shared context, coordination, or a shared task list, you MAY use parallel `Agent()` calls instead. But you MUST explain this choice to the user before proceeding.
3. **You are the team lead.** Do not delegate the lead role to another agent.
4. **Always use model: opus** for all teammates.
5. **Never spawn agents before the user approves the design.**

## Protocol

### Step 1 — Analyze the Task

Read the user's request carefully. Determine:
- What is the goal?
- What subtasks are involved?
- Which subtasks depend on each other vs. can run in parallel?
- Do agents need to share context or coordinate? (If yes → TeamCreate. If fully independent → Agent() may be acceptable.)

### Step 2 — Design the Team

Decide:
- **Team name**: short kebab-case name describing the project (e.g., `auth-refactor`, `new-feature-x`)
- **Number of agents**: minimum needed — do not over-engineer
- **Per agent**:
  - `name`: short descriptive name (e.g., `frontend-dev`, `api-builder`, `researcher`)
  - `subagent_type`: choose based on what tools the agent needs:
    - `general-purpose` — full access (read, write, edit, bash). Use for implementation work.
    - `Explore` — read-only. Use for research, codebase exploration, finding files.
    - `Plan` — read-only. Use for architecture planning, design reviews.
    - Custom agents from `.claude/agents/` if available and appropriate.
  - `role description`: 1-2 sentences of what this agent is responsible for
  - `isolation`: decide if the agent needs a worktree:
    - Use `worktree` when agents edit overlapping files or when you want clean diffs per agent
    - Skip worktree when agents work on completely separate files or do read-only work
- **Task breakdown**: list the tasks each agent will work on, including dependencies

### Step 3 — Present Design for Approval

Present the team design to the user using `AskUserQuestion` with a preview showing:

```
Team: {team-name}
Lead: You (Claude)

| # | Agent Name     | Type            | Isolation | Role                          |
|---|---------------|-----------------|-----------|-------------------------------|
| 1 | {name}        | {subagent_type} | {yes/no}  | {role description}            |
| 2 | {name}        | {subagent_type} | {yes/no}  | {role description}            |

Tasks:
1. [agent-name] {task description}
2. [agent-name] {task description} (blocked by #1)
3. [agent-name] {task description}
```

Ask: "Does this team design look good, or do you want changes?"

Options:
- "Looks good, proceed" — go to Step 4
- "I want changes" — ask what to modify, then re-present

### Step 4 — Create Team and Spawn

1. Use `TeamCreate` to create the team
2. Use `TaskCreate` to create all tasks in the shared task list
3. Spawn each teammate using the `Agent` tool with:
   - `team_name`: the team name
   - `name`: the agent name from the design
   - `subagent_type`: as designed
   - `model`: "opus" (always)
   - `isolation`: "worktree" if designed that way
   - `prompt`: detailed instructions including:
     - Their specific role and responsibilities
     - Which tasks they own (reference task IDs)
     - Key context about the codebase (relevant file paths, patterns)
     - How to coordinate with other teammates
     - Remind them to check TaskList after completing each task
4. Assign tasks to agents using `TaskUpdate` with `owner`

### Step 5 — Coordinate

As team lead:
- Monitor teammate messages (they arrive automatically)
- Reassign or unblock tasks as needed
- Answer teammate questions
- When all tasks are done, send shutdown messages to teammates
- Report results to the user

## When NOT to Use a Team

Use regular `Agent()` calls (not TeamCreate) when:
- The task has 1-2 **fully independent** subtasks with zero coordination needed
- Agents only need to research/read (no shared writes)
- The user explicitly asks for independent parallel agents

In this case, explain: "These subtasks are fully independent and don't need coordination, so I'll use parallel agents instead of a team."

## Anti-Patterns to Avoid

- **Never** spawn 3+ agents via parallel `Agent()` calls without TeamCreate
- **Never** skip the design approval step
- **Never** use subagent_type that can't do the required work (e.g., don't use `Explore` for implementation)
- **Never** create agents without clear task assignments
- **Never** use a model other than opus unless the user explicitly requests it
- **Never** spawn agents and then forget to coordinate — you are the lead, stay engaged
