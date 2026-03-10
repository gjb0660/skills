---
name: skill-evaluate
description: Evaluate a concrete request via skill-reviewer Evaluation Mode.
argument-hint: What request should be evaluated?
agent: agent
---
Related skill: `skill-reviewer`. Load and follow **Evaluation Mode** section for template and principles.

Arguments (MUST VALIDATE):

* evaluation request to execute explicitly

If the argument is missing or ambiguous, ask for the evaluation request via built-in question tool.

Delegate the evaluation workflow, comparison protocol, scoring assertions, and token accounting to skill-reviewer.

Prompt-specific rules:

1. State that the run is using Evaluation Mode.
2. Do not switch to Inspect Mode unless the user explicitly redirects you.
3. Do not restate or reimplement skill-reviewer's detailed evaluation protocol inside this prompt.
4. Keep the prompt layer minimal and let the skill own the heavy logic.

Remember to follow the `skill-reviewer` procedures in **Evaluation Mode** section.