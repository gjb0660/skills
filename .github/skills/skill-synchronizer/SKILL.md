---
name: skill-synchronizer
description: 'Synchronize maintained third-party skills from official upstream sources into this workspace. Use this skill when the user wants to install, update, refresh, or align a supported external skill with its upstream repository while preserving unrelated local files.'
---

Synchronize maintained third-party skills from official upstream sources into this workspace.

## Maintained Skills

| Skill | Upstream | Default target path |
| --- | --- | --- |
| `skill-creator` | https://github.com/anthropics/skills/tree/main/skills/skill-creator | `.github/skills/skill-creator/` |

## Defaults and scope

- Identify which maintained skill the user wants to synchronize before making changes.
- Use the upstream source listed in the maintained skills table for that skill.
- Treat this as a workspace-scoped skill operation for the current repository.
- Install or update the skill in its default target path unless the user explicitly asks for a different target path.
- Use a temporary workspace directory only (e.g., `.tmp/`) for download, extraction, or cache files, and remove it before finishing.
- Preserve unrelated skills, prompts, tests, and user changes outside the target skill directory.

## Execution workflow

1. Identify the maintained skill requested by the user and its target path.
2. Check whether the target directory already exists and inspect its contents.
3. Read the upstream files for that skill from the listed source.
4. Decide whether this run is a fresh install or an update.
5. If the skill is missing, add the upstream files locally.
6. If the skill already exists, update the local copy to match upstream while keeping the change scope limited to the target directory.
7. If meaningful local customizations already exist inside the target directory, summarize the differences and ask before overwriting them.
8. Validate that the resulting local skill has the expected upstream file structure.

## Guardrails

- Do not modify other skills or unrelated customization files.
- Do not synchronize skills that are not listed in the maintained skills table; summarize the mismatch and ask before proceeding.
- Do not invent missing upstream files; inspect the upstream repository when the structure is unclear.
- Prefer the smallest set of edits that makes the local skill align with upstream.
- If the user asks for a non-default target path, keep the same skill contents and only adjust the install location.
- Clean up temporary download, extraction, or cache files before finishing.

## Response requirements

- State whether the run performed an install or an update.
- State the maintained skill name and the local target path used.
- Summarize the files added, updated, or removed.
- Mention the upstream source inspected and any unresolved conflicts or follow-up actions.