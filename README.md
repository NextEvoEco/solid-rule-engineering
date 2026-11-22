# solid-rule-engineering
Evidence-based, read-only SOLID analysis that relates requirement semantics to object-oriented code structure.

## Codex skill

Copy the `skills/solid-rule-engineering` directory into your project's
`.agents/skills/` directory to make the skill available in that project.
Invoke it with a target and a task, for example:

> Use $solid-rule-engineering to map the requirements and change drivers for `InvoiceService.calculateTotal`, then review each applicable SRP rule without modifying code.

Version 0.2.0 covers semantic-first OO SOLID analysis at package, class, interface, and method levels. The skill guides requirement-to-code mapping, analysis, review, and proportional recommendations while loading only rules applicable to the target.

- [Skill instructions](skills/solid-rule-engineering/SKILL.md)
- [OO SOLID rules](skills/solid-rule-engineering/references/oo-solid-rules.md)
- [SRP rules](skills/solid-rule-engineering/references/srp-function-rules.md)
- [Example review and recommendation](examples/srp-function-review.md)
