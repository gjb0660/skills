---
name: skill-reviewer
description: "Review a skill as a specialist reviewer. Use this skill when you need a comprehensive skill health check, description strategy review, progressive-loading audit, or a visible with-skill vs without-skill evaluation. Use it because skill quality depends on reviewer-grade diagnosis, evidence, and human approval for key changes."
---

# Skill Reviewer

Choose the mode from the user's input.

- If the input names a target skill or clearly asks for a skill review, use **Inspect Mode**.
- If the input is an end-user request, benchmark request, or asks whether a skill helps, use **Evaluation Mode**.
- If both are ambiguous, ask a short clarifying question before proceeding.

Don't forget basic [Design Philosophy](./references/design-philosophy.md) when reviewing any skills.

## Professional Ethics

As a professional reviewer, You MUST:

- Avoid self-serving bias.
- Avoid misuse of tools.
- Maintain auditability.
- Maintain responsibility boundaries.

If performing evaluations of yourself, state that you are evaluating your own skill and be extra vigilant for bias, overfitting, and blind spots. Consider asking a human to review your evaluation before finalizing it.

## Shared Rules

1. State the selected mode before doing substantive work.
2. Prefer repository facts over assumptions. Read the target SKILL.md and only load extra references as needed.
3. Faith from the philosophy, follow the principles in [Design Philosophy](./references/design-philosophy.md).
4. Treat any risky, deceptive, security-harming, or capability-expanding behavior beyond the stated description as a severe finding.

## Reviewer Focus

Prioritize these reviewer concerns:

- discovery quality and trigger precision
- progressive disclosure and file weight
- behavior matching description
- system safety, explicit scope, and absence of surprise
- reusable guidance instead of test-case overfitting
- clear human checkpoints for high-impact decisions

---

## Inspect Mode

In this mode, perform a comprehensive health check for the named skill.

### Inspect Procedure

1. Load the target skill's SKILL.md.
2. Check the discovery layer:
   - metadata is present and coherent
   - description is roughly concise discovery text rather than a mini-manual
   - description explains function, trigger scenarios, imperative discovery phrasing, and why the skill should be used
3. Check the workflow layer:
   - SKILL.md body stays under 500 lines
   - long procedures, examples, or rubrics are delegated to references/
   - if the body is overloaded, recommend moving overflow into references/ and adding a short table of contents in SKILL.md
4. Perform a safety and scope audit:
   - flag malware, exploit, credential-harvesting, persistence, privilege-escalation, or covert-collection instructions
   - flag any behavior that exceeds the skill description or hides risky intent behind vague wording
   - treat these issues as blocking findings
5. Remove dead weight conceptually:
   - call out repetitive, unenforced, or non-operative text
   - identify content that does not affect invocation, behavior, or review quality
6. Evaluate the skill against the design philosophy in [inspect-checklist](./references/inspect-checklist.md).
7. Produce a lightweight health summary first, then findings ordered by severity, then concrete improvement directions.
8. When the fixes are local and clear, include a patch draft or replacement text snippet that the reviewer could apply.

### Inspect Output Format

Use this structure unless the user requested a different format:

1. Health Summary
2. Critical Findings
3. Safety and Scope Findings
4. Design Philosophy Assessment
5. Suggested Refactor Plan
6. Patch Draft
7. Open Questions

If there are no material issues, say so explicitly and mention any residual risk such as missing examples, missing references, or unclear triggers.

---

## Evaluation Mode

In this mode, evaluate whether a skill materially helps on a request and whether it behaves in a stable, auditable way.

### Evaluation Procedure

1. Determine the evaluation target from the request.
2. Infer the candidate skill if the user did not provide one explicitly. State the assumption explicitly in the report.
3. Classify the skill under evaluation:
   - Capability Uplift: should create a noticeable quality gap between with-skill and without-skill outputs
   - Encoded Preference: should enforce stable team conventions, formatting, policy, or workflow preferences
4. Check safety and surprise constraints before benchmarking:
   - do not benchmark a skill that contains malware, exploit steps, credential exfiltration, persistence, or hidden scope expansion as if it were a normal quality variant
   - report such behavior as a blocking failure of the skill design
5. Run two context-isolated executions in the same turn when tooling allows:
   - without skill
   - with skill
6. Prefer parallel execution for the two branches.
7. Compare the outputs using the rubric in [evaluation-rubric](./references/evaluation-rubric.md).
8. Write scoring assertions and a critical assessment of evaluation quality:
   - what the benchmark demonstrated
   - what it failed to demonstrate
   - whether the prompt was strong enough to expose the difference
   - whether the judged difference is robust or likely incidental

If isolated subagents are unavailable, explain the limitation briefly and run the cleanest possible sequential fallback while preserving the same audit structure.

### Evaluation Output Format

If no skill is actually invoked, say so explicitly in the final token report.

Recommended response structure:

1. Skill invocation notice
   Report the next skill name and why it is needed.
2. Skill execution
   Perform the requested task using the named skill.
3. Session token report
   Summarize token usage as a concise operational report, grouped by source and including skill-related overhead.

Keep the output format consistent with the evaluation prompt:

> ## Skill Invocation Notice
> 
> - Skill: <name>
> - Reason: <why this skill is being used now>
> 
> ## Execution Result
> 
> Wrap the substantive result in a code block, especially when it is multi-line > or structured.
> 
> ## Session Token Report
> 
> Include these line items:
> 
> * User request tokens: <exact number or estimated like `≈150`>
> * Workspace context tokens: <exact number or estimated like `≈420`>
> * Skill invocation tokens: <exact number or estimated like `≈90`>
> * Tool retrieval tokens: <exact number or estimated like `≈210`>
> * Final response tokens: <exact number or estimated like `≈260`>
> * Total input tokens: <exact number or estimated like `≈870`>
> * Total output tokens: <exact number or estimated like `≈260`>
> * Input/output ratio: <exact ratio or estimated like `≈3.3:1`>
> * Total session tokens: <exact number or estimated like `≈1130`>
> * Notes: <one short note on missing data, estimation method, or what is excluded>
>

Guidance:

* Prefer source-based accounting over vague buckets such as generic reasoning tokens unless the environment exposes them directly.
* If exact token data is unavailable, use an estimated value with the `≈` prefix instead of `unavailable`, and add one short note explaining what is estimated versus directly observed.

Be strict about the reporting requirements, but keep the execution itself concise and task-focused.

---

## References

- [Design Philosophy](./references/design-philosophy.md)
- [Inspect checklist](./references/inspect-checklist.md)
- [Evaluation rubric](./references/evaluation-rubric.md)