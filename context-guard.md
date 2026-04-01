---
name: context-guard
description: Always-active context window guardian. When context window usage exceeds 80%, pause before starting any non-trivial task and ask the user whether to delegate it to a subagent or continue in the main session. Never auto-delegate — always ask first. Triggers on every user request when context is high.
---

# Context Guard

## Rule

Before starting any task, check the current context window `used_percentage` from session data.

**If usage > 80%:** Stop. Do not start the task. Ask the user:

> "Context is at X% — want me to handle this in a subagent to keep the main session clean, or continue here?"

Wait for their decision before doing anything.

**If usage ≤ 80%:** Proceed normally. Do not mention context at all.

## What counts as non-trivial (ask before doing at >80%)

- Multi-step implementation or refactoring
- Codebase exploration (multiple file reads, greps, glob searches)
- Web research
- Running tests or builds
- Any task likely to generate large output

## What does NOT need a check (proceed directly even at >80%)

- Single file reads
- Short factual questions
- One-liner tool calls

## If user says "use a subagent"

Delegate via the Agent tool. Always instruct the subagent to return a **concise summary only** — not raw output — to avoid consuming main session context on the return.
