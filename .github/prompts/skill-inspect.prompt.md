---
name: skill-inspect
description: "Inspect a specific skill with mandatory pre-invocation reporting and end-of-session token accounting."
argument-hint: "What skill are you inspect, or what is the evaluate request?"
agent: agent
---

Run the requested task as a skill evaluate session.

Treat the prompt arguments as:

* target skill name
* or evaluate request to execute explicitly

If no arguments are provided, you MUST proactively ask the user for the missing information.

Your job is to evaluate the skill in a visible, auditable way.

Requirements:

1. Before each skill invocation, explicitly report:
   * the skill name you are about to use
   * the reason this skill is the correct choice for the next step
2. If the task requires multiple skill invocations in one response, repeat that report before each invocation.
3. Wrap the execution result in a code block for clarity, especially if it includes structured data or multiple lines.
4. At the end of the session, include a token usage report.
   * The token usage report must include a separate line item for skill-related token usage.
   * Prefer practical, source-oriented token categories that help a human reviewer quickly understand where session cost came from.
5. The report should prioritize these categories when available:
   * user request tokens
   * workspace or file-context tokens
   * skill invocation overhead tokens
   * tool or retrieval tokens
   * final response tokens
   * total input tokens
   * total output tokens
   * input/output ratio

Hard rules:

* Do not silently invoke a skill.
* Do not omit the reason for the invocation.
* Do not invent exact token numbers if they are not available from the environment.
* If exact token data is unavailable, clearly label each number as estimated (e.g. `≈150`).
* If no skill is actually invoked, say so explicitly in the final token report and record skill invocation tokens as `0` or an estimated value with the `≈` prefix, depending on what the environment can support.

Recommended response structure:

1. Skill invocation notice
   Report the next skill name and why it is needed.
2. Skill execution
   Perform the requested task using the named skill.
3. Session token report
   Summarize token usage as a concise operational report, grouped by source and including skill-related overhead.

Use this output format:

## Skill Invocation Notice

- Skill: <name>
- Reason: <why this skill is being used now>

## Execution Result

<result>

## Session Token Report

* User request tokens: <exact number or estimated like `≈150`>
* Workspace context tokens: <exact number or estimated like `≈420`>
* Skill invocation tokens: <exact number or estimated like `≈90`>
* Tool retrieval tokens: <exact number or estimated like `≈210`>
* Final response tokens: <exact number or estimated like `≈260`>
* Total input tokens: <exact number or estimated like `≈870`>
* Total output tokens: <exact number or estimated like `≈260`>
* Input/output ratio: <exact ratio or estimated like `≈3.3:1`>
* Total session tokens: <exact number or estimated like `≈1130`>
* Notes: <one short note on missing data, estimation method, or what is excluded>

Guidance:

* Prefer source-based accounting over vague buckets such as generic reasoning tokens unless the environment exposes them directly.
* If exact token data is unavailable, use an estimated value with the `≈` prefix instead of `unavailable`, and add one short note explaining what is estimated versus directly observed.

Be strict about the reporting requirements, but keep the execution itself concise and task-focused.