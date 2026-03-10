---
name: skill-inspector
description: "Inspect or evaluate a skill. Use this skill when you need a comprehensive skill health check, description strategy review, progressive-loading audit, or a visible with-skill vs without-skill comparison. Use it because skills alter agent behavior and should be reviewed with explicit evidence, mode-aware scoring, and human approval for key decisions."
argument-hint: "Provide a skill name for Inspect Mode, or an evaluation request for Evaluation Mode"
---

# Skill Inspector

Use this skill for two different but related jobs:

- Inspect Mode: audit an existing skill definition and explain what should change.
- Evaluation Mode: evaluate skill impact in a visible, auditable way.

Keep the work concise, evidence-based, and reviewable.

## Mode Selection

Choose the mode from the user's input.

- If the input names a target skill or clearly asks for a skill review, use Inspect Mode.
- If the input is an end-user request, benchmark request, or asks whether a skill helps, use Evaluation Mode.
- If both are ambiguous, ask a short clarifying question before proceeding.

## Shared Rules

1. State the selected mode before doing substantive work.
2. Prefer repository facts over assumptions. Read the target SKILL.md and only load extra references as needed.
3. Keep the review aligned with progressive disclosure:
   - frontmatter and description are the discovery layer
   - SKILL.md body is the workflow layer
   - references/ holds long checklists, examples, or rubrics
4. Do not silently rewrite another skill during inspection. Diagnose first; include a patch draft by default when useful, but edit the actual files only if the user explicitly asks.
5. Favor explanations of why a design helps agent behavior instead of turning the report into rigid rule recitation.
6. Treat any risky, deceptive, or capability-expanding behavior beyond the stated description as a severe finding.
7. In Inspect Mode, include a concrete patch draft by default when the problems are actionable from the inspected files.

---

## Inspect Mode

In this mode, perform a comprehensive health check for the named skill.

### Procedure

1. Load the target skill's SKILL.md.
2. Check the discovery layer:
   - metadata is present and coherent
   - description is roughly concise discovery text rather than a mini-manual
   - description explains function, trigger scenarios, imperative discovery phrasing, and why the skill should be used
3. Check the workflow layer:
   - SKILL.md body stays under 500 lines
   - long procedures, examples, or rubrics are delegated to references/
   - if the body is overloaded, recommend moving overflow into references/ and adding a short table of contents in SKILL.md
4. Remove dead weight conceptually:
   - call out repetitive, unenforced, or non-operative text
   - identify content that does not affect invocation, behavior, or review quality
5. Evaluate the skill against the design philosophy in [inspect-checklist](./references/inspect-checklist.md).
6. Produce a lightweight health summary first, then findings ordered by severity, then concrete improvement directions.
7. When the fixes are local and clear, include a patch draft or replacement text snippet that the reviewer could apply.

### Inspect Output Shape

Use this structure unless the user requested a different format:

1. Health Summary
2. Critical Findings
3. Design Philosophy Assessment
4. Suggested Refactor Plan
5. Patch Draft
6. Open Questions

If there are no material issues, say so explicitly and mention any residual risk such as missing examples, missing references, or unclear triggers.

---

## Evaluation Mode

In this mode, evaluate whether a skill materially helps on a request and whether it behaves in a stable, auditable way.

### Mandatory Reporting

Before each skill invocation, explicitly report:

- Skill: the skill name you are about to use
- Reason: why this skill is the correct choice for the next step

If no skill is actually invoked, say so explicitly in the final token report.

### Procedure

1. Determine the evaluation target from the request.
2. Infer the candidate skill if the user did not provide one explicitly. State the assumption explicitly in the report.
3. Classify the skill under evaluation:
   - Capability Uplift: should create a noticeable quality gap between with-skill and without-skill outputs
   - Encoded Preference: should enforce stable team conventions, formatting, policy, or workflow preferences
4. Run two context-isolated executions in the same turn when tooling allows:
   - without skill
   - with skill
5. Prefer parallel execution for the two branches.
6. Compare the outputs using the rubric in [evaluation-rubric](./references/evaluation-rubric.md).
7. Write scoring assertions and a critical assessment of evaluation quality:
   - what the benchmark demonstrated
   - what it failed to demonstrate
   - whether the prompt was strong enough to expose the difference
   - whether the judged difference is robust or likely incidental

If isolated subagents are unavailable, explain the limitation briefly and run the cleanest possible sequential fallback while preserving the same audit structure.

### Evaluation Output Format

Keep the output format consistent with the existing skill-evaluation prompt:

## Skill Invocation Notice

- Skill: <name>
- Reason: <why this skill is being used now>

## Execution Result

Wrap the substantive result in a code block, especially when it is multi-line or structured.

## Session Token Report

Include these line items:

- User request tokens
- Workspace context tokens
- Skill invocation tokens
- Tool retrieval tokens
- Final response tokens
- Total input tokens
- Total output tokens
- Input/output ratio
- Total session tokens
- Notes

Never invent exact token values. If exact numbers are unavailable, mark them as estimated with the ≈ prefix and keep the estimation method short and practical.

Do not collapse the judgment into a single overall score. Report per-dimension scores and then state the final evaluation assertion in prose.

## Completion Criteria

The skill run is complete when:

- the correct mode was selected and stated
- the relevant evidence was actually inspected or executed
- the report includes concrete findings or a justified pass result
- Evaluation Mode includes explicit invocation notices and token accounting
- recommendations distinguish between must-fix risks, quality improvements, and optional cleanup

## References

- [Inspect checklist](./references/inspect-checklist.md)
- [Evaluation rubric](./references/evaluation-rubric.md)