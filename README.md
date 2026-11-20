# solid-rule-engineering
Executable SOLID rules, evidence requirements, and acceptance criteria for AI-generated code.

## Codex skill

Copy the `skills/solid-rule-engineering` directory into your project's
`.agents/skills/` directory to make the skill available in that project.
Invoke it with a target and a task, for example:

> Use $solid-rule-engineering to review `InvoiceService.calculateTotal` and its callers. Report the evidence for each applicable rule.

Version 0.1.0 covers function- and method-level SRP. The skill guides analysis,
implementation, and verification using the target repository's existing tools.
The rule pack defines evidence requirements and acceptance criteria.

- [Skill instructions](skills/solid-rule-engineering/SKILL.md)
- [SRP rules](skills/solid-rule-engineering/references/srp-function-rules.md)
- [Example review and refactor](examples/srp-function-review.md)
