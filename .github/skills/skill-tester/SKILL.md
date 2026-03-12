---
name: skill-tester
description: Run visible, auditable skill tests and manage skill test cases under tests/test-*.md.
---

# Skill Tester

Use this skill to test skill definitions in the current repository and to keep the full test workflow visible, auditable, and reproducible.

This skill is generic. Keep the skill body limited to repository-wide testing rules and test-case management instructions. Put all skill-specific behavior, scenarios, and assertions in the corresponding test case file.

## Repository Conventions

- Skill definitions live in `skills/<skill-name>/SKILL.md`.
- Skill-specific test cases live in `tests/test-<skill-name>.md`.
- Temporary artifacts for a test live in `.tmp/<skill-name>/test/`.

## Responsibilities

This skill has two responsibilities:

1. Execute a skill test end to end.
2. Create, review, update, list, or remove skill test cases when the user asks for case maintenance.

In both modes, the current workspace is the source of truth. Never rely on stale context when files may have changed.

## Discovery Rules

1. Scan `tests/` for files matching `test-*.md`.
2. Derive the target skill name from the file name: `tests/test-<skill-name>.md` maps to `<skill-name>`.
3. If the user names a specific skill, operate only on that case.
4. If the user asks to test all skills or list all cases, collect every matching case.
5. If a requested case or skill file is missing, report the exact missing artifact instead of inventing one.

## Execution Workflow

### 1. Sync Current State

- Re-read the target skill file and the corresponding test case before acting.
- Inspect the matching temp directory for existing files or user edits.
- Treat current workspace contents as authoritative.

### 2. Make The Invocation Explicit

Before invoking the skill under test, explicitly state:

- `Skill: <skill-name>`
- `Reason: <why this skill is needed for the current step>`

Do not invoke the tested skill silently.

### 3. Execute The Case

- Follow the test case exactly.
- Keep all temporary test artifacts inside `.tmp/<skill-name>/test/` unless the case explicitly requires something else.
- If existing files were manually edited, continue from the current state with the smallest necessary patch.
- Do not rewrite a user-modified file when a local patch is sufficient.

### 4. Verify Minimally

- Perform the smallest direct verification that proves the case outcome.
- Prefer concrete checks such as running a script, checking a created file, confirming a TODO was completed, or verifying that no out-of-scope file was changed.
- If automatic verification is not possible, say why and provide auditable evidence instead of guessing.

### 5. Report The Result

Always report:

1. Test target
2. Case file used
3. Temp directory used
4. Key execution result
5. Verification result
6. Failures, blockers, or residual risks

## Test Case Management

When the user asks to create, review, update, list, or delete test cases, apply these rules.

### List Cases

- Discover all `tests/test-*.md` files.
- Report which skills already have cases and which requested ones are missing.

### Create A Case

- Create `tests/test-<skill-name>.md` only when the user requests a new case or a missing case must be added.
- Use the shared case format with top-level metadata bullets for `skill` and `tmpdir`.
- Keep the case focused on skill-specific behavior, scenario setup, assertions, and verification guidance.
- Do not duplicate generic testing workflow from this skill into the case.

### Review A Case

- Check whether the case is specific enough to test the target skill.
- Remove generic workflow text that belongs in this skill.
- Flag ambiguity, untestable assertions, mixed responsibilities, or instructions that would force writes outside the allowed temp directory without justification.

### Update A Case

- Preserve the existing intent unless the user asks to change it.
- Apply the smallest edit that improves clarity, scope, and auditability.
- Use referring back to `tmpdir` inside the scenario when that keeps the case concise.
- Keep skill-specific instructions in the case and generic process rules in this skill.

### Delete A Case

- Delete a case only when the user explicitly requests removal.
- Prefer also confirming whether the matching temp directory should be removed.

## Recommended Case Template

When creating or heavily rewriting a test case, use the shared template in [references/test-template.md](./references/test-template.md).

Keep the final case focused on the target skill by replacing the template guidance with concrete, skill-specific scenario details, assertions, verification steps, and pass criteria.

## Output Format

### Test Target

- Skill: `<skill-name>`
- Case: `tests/test-<skill-name>.md`
- TmpDir: `.tmp/<skill-name>/test/`

### Execution

- Summarize the key actions taken.

### Verification

- List the verification actions and their results.

### Result

- `PASS` or `FAIL`
- If failed, give the smallest blocking reason.

## Quality Bar

- Sync before acting.
- Keep the process visible, auditable, and reproducible.
- Do not fabricate files, outputs, or verification evidence.
