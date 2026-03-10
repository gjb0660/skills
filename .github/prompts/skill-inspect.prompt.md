---
name: skill-inspect
description: Inspect a named skill via skill-reviewer Inspect Mode.
argument-hint: Which skill should be inspected?
agent: agent
---
Related skill: `skill-reviewer`. Load and follow **Inspect Mode** section for template and principles.

Arguments (MUST VALIDATE):

* target skill name specified explicitly

If the argument is missing or ill-formed, ask for the target skill name via built-in question tool.

Delegate the inspection workflow, report structure, token accounting, and patch-draft behavior to skill-reviewer.

Prompt-specific rules:

1. State that the run is using Inspect Mode.
2. Do not switch to Evaluation Mode unless the user explicitly redirects you.
3. Do not restate or reimplement skill-reviewer's detailed checklist inside this prompt.
4. Keep the prompt layer minimal and let the skill own the heavy logic.

Remember to follow the `skill-reviewer` procedures in **Inspect Mode** section.