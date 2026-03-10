# Inspect Checklist

Use this checklist when reviewing a skill in Inspect Mode.

## 1. Discovery Layer

- Name matches the folder name.
- Description is concise discovery text rather than a long tutorial.
- Description states what the skill does.
- Description enumerates when the skill should trigger.
- Description uses imperative discovery phrasing such as "Use this skill when..."
- Description explains why the agent should trigger it, not only what it does.
- Argument hint is present when the slash entry needs non-obvious input.

## 2. Workflow Layer

- SKILL.md body stays under 500 lines.
- Long examples, rubrics, or protocol details are moved into references/.
- SKILL.md has a clear top-level structure and quick scan path.
- If the skill is long, SKILL.md includes a short table of contents or a compact section map.
- Steps are actionable and correspond to observable behavior.

## 3. Content Quality

- Remove text that does not change behavior, discovery, or review quality.
- Remove repeated warnings stated in multiple ways.
- Remove decorative theory that never affects execution.
- Keep examples only when they clarify a decision or format.

## 4. Design Philosophy

### Progressive Disclosure

- Discovery information is in frontmatter.
- Core workflow stays in SKILL.md.
- Heavy detail is delegated to references/.

### Principle of Lack of Surprise

- The skill does not ask the agent to perform hidden actions.
- The real behavior does not exceed the advertised behavior.
- The skill does not include malware, exploit code, or instructions that would compromise system safety.

### Explain Why, Not Only Must

- Important constraints include rationale.
- The wording guides reasoning instead of relying only on rigid uppercase mandates.

### Generalize, Don't Overfit

- The skill teaches a reusable workflow.
- It does not appear narrowly tuned to one test case or one file.

### Human in the Loop

- Repetitive work can be automated.
- Key decisions, rewrites, or risky actions are surfaced for human review.

## 5. Reporting Expectations

- Start with a brief health summary.
- Order findings by severity.
- Distinguish hard risks from style improvements.
- If suggesting refactors, explain which content should move into references/ and why.
- When the remedy is clear, attach a patch draft or replacement snippet instead of stopping at abstract advice.