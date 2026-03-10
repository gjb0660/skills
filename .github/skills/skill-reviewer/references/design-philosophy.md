# Design Philosophy

```
skill-name/
├── SKILL.md (required)
│   ├── YAML frontmatter (name, description required)
│   └── Markdown instructions
└── Bundled Resources (optional)
   ├── scripts/    - Executable code for deterministic/repetitive tasks
   ├── references/ - Docs loaded into context as needed
   └── assets/     - Files used in output (templates, icons, fonts)
```

1. **Progressive Disclosure**
   Keep a three-layer loading model:
   - Metadata (name + description) - Always in context (~100 words)
   - SKILL.md body - In context whenever skill triggers (<500 lines ideal)
   - Bundled resources - As needed (unlimited, scripts can execute without loading)

2. **Principle of Lack of Surprise**
   The skill must not contain malware, exploit code, persistence tricks, credential harvesting steps, or any behavior that would harm the system or exceed the described scope. Security-sensitive behavior that is not clearly disclosed is a blocking problem, not a style issue.

3. **Explain Why, Not Only Must**
   Prefer rationale, review logic, and decision criteria over rigid command language. Constraints should teach the reviewer how to reason, not only what to repeat.

4. **Generalize, Don't Overfit**
   Improve the workflow based on reusable patterns. Do not tune the skill narrowly for one benchmark, one repository quirk, or one test case.

5. **Human in the Loop**
   Automate repetitive checking and formatting work, but keep structural rewrites, risky actions, and benchmark conclusions visible for human approval.
