---
description: Run or continue the Growth OS for Claude Cowork Quick Start setup
allowed-tools: Read, Write, Edit, WebSearch, WebFetch, Bash, AskUserQuestion
argument-hint: [resume]
---

Read the quick-start skill at `${CLAUDE_PLUGIN_ROOT}/skills/quick-start/SKILL.md` and follow its instructions.

If a `progress.md` file exists in the workspace root, read it first to determine where the user left off and resume from there.

If no `progress.md` exists, start from the beginning (Phase 1: Quick Intake).

If the user passed "resume" as an argument, explicitly tell them where they are in the process before continuing.
