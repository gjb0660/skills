# Continue Skill Test Case

- skill: `continue`
- tmpdir: `tests/test-continue/`

## Scenario

- Exercise the skill against a small Python script inside **tmpdir**.
- Initial run: create or update the script so it is runnable and prints `Hello world` with no arguments.
- Follow-up run: after the user manually edits that script and asks to `continue`, the agent must sync the current file state first and then apply only the smallest patch needed for the requested change.

## Preconditions

- The test may begin with an empty temp directory or with an existing user-edited script.
- The current contents of **tmpdir** are the source of truth for every continuation step.

## Skill-Specific Assertions

- After the initial execution, **tmpdir** contains a runnable Python script.
- Running the script without extra input prints `Hello world`.
- On a follow-up `continue` request, the agent re-reads the current script before editing it.
- Follow-up edits preserve the user-modified structure and apply only the minimum necessary patch.
- Any artifacts created during the test stay inside **tmpdir**.

## Suggested Verification

- Run the script and confirm the default output includes `Hello world`.
- For a later continuation that adds a small behavior change, run the updated script again and verify that only the requested behavior changed.
- Inspect the resulting edit and confirm it patched the current file in place instead of replacing it wholesale.

## Pass Criteria

- The initial script is created or validated successfully.
- A later continuation respects user edits and updates the existing script in place.
- The execution record, verification steps, and result remain explicit and auditable.