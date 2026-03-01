# Agentic Coding Templates

A dead-simple AI layer for building anything with Claude Code. No over-engineering, no complex multi-agent frameworks — just a reliable, repeatable workflow you can make your own.

Inspired by this [YouTube video](https://youtu.be/goOZSXmrYQ4). For the reasoning behind the workflow, see [CONCEPTS.md](./CONCEPTS.md).

## What's included

```
.claude/
  CLAUDE-template.md     ← Template for your global rules file
  PRD-example.md         ← Example of a completed PRD
  commands/
    prime.md             ← /prime         — Run at the start of every session
    create-prd.md        ← /create-prd    — Generate a structured PRD from conversation
    create-rules.md      ← /create-rules  — Generate your CLAUDE.md global rules
    plan-feature.md      ← /plan-feature  — PIV loop step 1: plan with tasks + validation
    execute.md           ← /execute       — PIV loop step 2: implement from plan file
    commit.md            ← /commit        — Standardized commit messages
    init-project.md      ← /init-project  — Bootstrap a new project
```

## The PIV Loop

**Plan → Implement → Validate** — the core workflow for every feature.

```
1. /prime            → Catch up on codebase, identify next phase from PRD
2. Vibe planning     → Casual conversation about the feature (sub-agents for research)
3. /plan-feature     → Create structured plan with tasks + validation strategy
                        Saved to .agents/plans/<feature>.md
4. [New session]     → Context reset — keep it clean before implementation
5. /execute [plan]   → Agent implements everything, runs tests, validates
6. Human validate    → Code review + manual smoke test
7. /commit           → Standardized commit for a clean git history
```

## The Four Golden Rules

1. **Context is your most precious resource** — Reset between planning and implementation
2. **Commandify everything** — If you do it twice, make it a command
3. **Commit history is long-term memory** — Standardized messages help the agent orient itself on `prime`
4. **System evolution mindset** — Every bug is an opportunity to improve your AI layer

## How to use

Copy the `.claude/` folder into your project and start with:

```
/init-project
```

or if you already have an idea:

```
/create-prd
```

Adapt the commands to your stack over time. The point is to make this **your own**.

## The AI Layer

Your AI layer consists of three things:

- **PRD** — What you're building
- **CLAUDE.md** — How to build it (rules, patterns, tech stack)
- **Commands** — Reusable workflows (prime, plan, execute, commit)

Keep `CLAUDE.md` concise. Use on-demand context files (e.g. `reference/components.md`) for deeper guidance that only loads when needed — progressive disclosure keeps your context clean.
