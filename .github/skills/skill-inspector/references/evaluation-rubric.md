# Evaluation Rubric

Use this rubric in Evaluation Mode.

## 1. Classify the Skill

### Capability Uplift

Use this category when the skill should noticeably improve problem solving quality, structure, or task coverage.

Judge primarily on:

- output quality gap between without-skill and with-skill
- completeness and correctness
- better decomposition, reasoning, or evidence use
- whether the uplift remains visible beyond one lucky prompt

### Encoded Preference

Use this category when the skill mainly encodes conventions, review standards, format rules, or workflow preferences.

Judge primarily on:

- stable compliance with the intended convention
- reduced drift across runs
- clear adherence to team-specific policy or formatting expectations
- whether the skill reduces ambiguity instead of just making the answer longer

## 2. Core Scoring Dimensions

Score each dimension on a simple 1-5 scale with one sentence of justification.

- Task fit: Did the selected skill match the request?
- Output quality: Was the with-skill result better on the task itself?
- Behavioral compliance: Did the result follow the intended workflow or standard?
- Evidence and auditability: Could a reviewer understand why the judgment was made?
- Robustness: Does the observed difference look repeatable rather than accidental?

Do not compute a synthetic overall total unless the user explicitly asks for one. The default output is dimension scores plus a written assertion.

## 3. Scoring Assertions

After scoring, make explicit assertions such as:

- "The skill produced a material uplift"
- "The skill improved compliance but not core task quality"
- "The observed difference is weak and may be prompt-sensitive"
- "The benchmark does not isolate the skill effect well enough"

## 4. Critical Evaluation Quality Check

Critique the benchmark itself.

- Was the request strong enough to trigger the skill naturally?
- Did the without-skill branch remain clean and not inherit hidden context?
- Did the with-skill branch actually use the intended skill rather than generic reasoning?
- Were there confounders such as different retrieved files, extra assumptions, or broader context?
- Does the result justify confidence, or should the benchmark be rerun with a sharper prompt?

## 5. Token Reporting

Prefer exact numbers when the environment exposes them.

If not available:

- use approximate values with the ≈ prefix
- separate skill invocation overhead from general tool retrieval
- include one short note describing what was estimated