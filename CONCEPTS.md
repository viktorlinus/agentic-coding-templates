# Core Concepts

The ideas behind this workflow — why it works and how to think about it.

## 1. Reduce Assumptions

> "One bad line in a PRD could be a thousand bad lines of code."

The #1 cause of bad AI-generated code isn't bad code — it's misalignment. When your agent makes an assumption about what you want, it can silently build the wrong thing for hundreds of lines.

**How to fix it:** After your initial brain dump, tell the agent to ask you a bunch of questions before doing anything. Claude Code's `ask_user` tool is great for this — it presents multiple choice options and covers edge cases you wouldn't have thought to specify yourself. Every question answered removes an assumption.

The conversation is unstructured context. The PRD is the only thing that survives. Make sure everything important from that conversation ends up in the PRD.

---

## 2. Context is Precious

Your agent's context window is a limited, shared resource. Everything loaded into it competes for attention and adds noise.

**Two rules:**
- **Reset between planning and execution.** Have the full planning conversation, create the structured plan, then start a fresh session with only the plan file. This keeps implementation focused and avoids stale context polluting the output.
- **Use on-demand context.** Don't dump everything into `CLAUDE.md`. Instead, point to secondary files that the agent reads only when relevant (e.g. "when working on the frontend, read `reference/components.md`"). This is progressive disclosure — the agent loads what it needs, when it needs it.

---

## 3. Sub-agents for Research, Not Implementation

Sub-agents are great for research because they load massive amounts of context (docs, web pages, codebase exploration) and return only a summary. Your main context stays clean.

**Don't use sub-agents for implementation.** Implementation depends on the accumulated context of everything you've been building — which files changed, what patterns you're following, what decisions were made. Sub-agents lose that thread and hallucinate more as a result. This is also why Claude Code's built-in sub-agents are research-only.

---

## 4. Set Up Env Vars Before Execution

If your project needs environment variables and they aren't set before the agent starts implementing, it will write mock tests that pass against nothing real. You'll think everything works — it doesn't.

Set up your `.env` file **in parallel with the planning phase**, before you ever run `/execute`.

---

## 5. Git Log is Long-Term Memory

The agent can't remember previous sessions. But it can read `git log`.

Standardized commit messages (via `/commit`) give the agent a timeline of what was built and when. On `/prime`, the agent reads the recent git log to orient itself — what phase are we on, what was the last thing built, what patterns are being used.

Sloppy commit messages = agent flying blind at the start of every session.

---

## 6. System Evolution Mindset

Every time something goes wrong — a bug, a style issue, a misunderstanding — ask yourself:

> "What can I change in my AI layer so this doesn't happen again?"

Maybe your `CLAUDE.md` needs a new rule. Maybe you need a new on-demand context file for a specific part of the codebase. Maybe a command needs to be more specific.

You're building three things in parallel:
- The **codebase**
- The **test suite**
- The **AI layer**

All three compound over time. A better AI layer means faster, more reliable PIV loops on every future feature.

---

## 7. Vibe Planning → Structured Plan

Start every feature with an unstructured conversation. Just talk — explore ideas, ask for sub-agent research, think out loud. This is "vibe planning."

Then turn that conversation into a structured plan with `/plan-feature`. The plan should include:
- Clear goal and success criteria
- Task list with specific files to create/edit
- **Validation strategy** — how to verify it works before you even write a line of code

The plan is what you hand to the execution agent. The conversation is disposable.

---

## 8. Regression Testing

After each PIV loop, consider what end-to-end tests should exist to make sure the thing you just built keeps working as you add more features.

You can build this into a command that re-runs a set of user journeys, or use an external tool. Either way — don't skip it. The cost of a broken previous feature discovered three loops later is much higher than writing the test now.
