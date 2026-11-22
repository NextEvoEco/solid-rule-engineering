# Codex installation

Install from the repository root:

```sh
codex skill install .
```

Codex reads `SKILL.md` at the repository root and resolves `references/`
relative paths automatically.

To invoke the skill within a task:

```text
$solid-rule-engineering
```

Or with a scope:

```text
Use $solid-rule-engineering to review src/orders/ for SRP and OCP.
```
