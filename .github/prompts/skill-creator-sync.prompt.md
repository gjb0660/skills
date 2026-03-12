---
name: skill-creator-sync
description: Install or update the official skill-creator skill from anthropics/skills into this workspace.
argument-hint: Optional: target path or special update constraints
agent: agent
---
Related skill: `skill-synchronizer`. Load and follow it.

Synchronize the maintained third-party skill `skill-creator`.

Arguments (MUST VALIDATE):

* optional target path or special sync constraint

If no argument, synchronize `skill-creator` into its default target path.

Prompt-specific rules:

- Keep the invocation interface unchanged.
- Preserve unrelated skills, prompts, tests, and user changes outside the target skill directory.

Remember use `skill-synchronizer` on the skill `skill-creator` to perform actual install or update, and keep the final response format unchanged.