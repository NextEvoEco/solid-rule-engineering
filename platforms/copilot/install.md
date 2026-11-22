# Copilot installation

GitHub Copilot reads `.github/copilot-instructions.md` as custom instructions.
Because Copilot cannot follow relative file references at runtime, generate a
single flat file before committing.

## Generate the flat file

Run from the repository root (requires `cat` or PowerShell):

```powershell
# PowerShell
@(
  Get-Content SKILL.md
  "`n---`n"
  Get-Content references/rule-schema.md
  "`n---`n"
  Get-Content references/oo-solid-rules.md
  "`n---`n"
  Get-Content references/srp-function-rules.md
  "`n---`n"
  Get-Content references/acceptance-report.md
) | Set-Content .github/copilot-instructions.md -Encoding utf8
```

## Keep the generated file in sync

Re-run the script whenever `SKILL.md` or any `references/` file changes.
Do not edit `.github/copilot-instructions.md` by hand; edit the source files
instead.

## Canonical source

`SKILL.md` and `references/` at the repository root are the canonical source.
The generated `.github/copilot-instructions.md` is a derived artifact.
