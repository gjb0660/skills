# Skill Test Case Template

Use this structure when creating or heavily rewriting a skill test case.

- skill: `<skill-name>`
- tmpdir: `.tmp/<skill-name>/test/`

## Scenario

- The skill-specific task or workflow to exercise.

## Preconditions

- Any relevant starting state that matters only for this skill.

## Skill-Specific Assertions

- Observable behaviors that must hold for this skill.

## Suggested Verification

- Minimal checks that prove the assertions.

## Pass Criteria

- Clear pass/fail conditions for the scenario.