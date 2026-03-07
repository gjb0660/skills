---
name: continue
description: Follow human-in-the-loop coding workflow only explicitly instructed to continue
---

# Human-in-the-loop Coding Workflow

Do not use this skill for normal new requests, generic Q&A, or unrelated fresh tasks.

This skill is for a human-in-the-loop coding workflow where the agent must first inspect the current workspace, detect developer changes, infer the updated design constraints, and only then continue implementation with minimal patches.

The **current workspace code is the source of truth**.

* Humans decide architecture and design.
* The AI agent assists with implementation.
* Manual code changes always take priority.

If the code differs from previous AI output, assume the developer **intentionally modified it**.

Never revert manual modifications unless explicitly instructed.

## Workflow

1. Sync
   Re-read the relevant current workspace files before proposing changes.
   Assume manual modifications may exist.
   Do not rely on earlier generated versions if they conflict with the current code.

2. Detect Changes
   Identify signs of developer edits, such as:
   * API or naming changes
   * ownership or memory model updates
   * module structure adjustments
   * initialization or lifecycle changes
   * comments or TODOs added by the developer
   Briefly summarize only the changes that matter to the continuation task.

3. Infer Rules
   Infer the developer's current design intentions from the code.
   Examples:
   * ownership model
   * module boundaries
   * lifecycle assumptions
   * project coding style
   Treat these as **constraints** for the continuation.

4. Plan
   Explain the **minimal changes** required to continue from the current state.
   Avoid refactoring unrelated code.
   Preserve existing structure, naming, and architecture unless the user asks otherwise.

5. Patch
   Modify the implementation **in place**.
   Rules:
   * respect manual modifications
   * keep architecture unchanged unless explicitly requested
   * apply small patches instead of rewrites
   * prefer continuing the developer's direction over restoring an older AI direction
   If uncertain, ask before making large changes.

## Output Format

Adapt the response to the complexity of the continuation.

For simple follow-up edits:

* give a brief current-state summary only if it affects the task
* state the next minimal change
* implement it directly

For non-trivial continuation tasks, use this structure:

1. Current-state findings
   Summarize only the developer changes that matter to the task.
2. Inferred constraints
   State the design rules or assumptions that must be preserved.
3. Minimal continuation plan
   Describe the smallest safe change that moves the task forward.
4. Implementation result
   Apply the patch and briefly note what changed, or state the blocker.

Do not add ceremony for its own sake.

If no meaningful changes were detected, keep the findings brief and move directly to the minimal plan.

The goal is to preserve the developer's direction while keeping the response concise and actionable.
