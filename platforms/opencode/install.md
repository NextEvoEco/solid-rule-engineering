# OpenCode installation

Place the skill directory where OpenCode resolves skills, then reference it
in your OpenCode configuration:

```jsonc
// opencode.json
{
  "skills": [
    "./path/to/solid-rule-engineering"
  ]
}
```

OpenCode reads `SKILL.md` at the skill root and resolves `references/`
relative paths automatically.

To invoke within a session:

```text
$solid-rule-engineering
```
