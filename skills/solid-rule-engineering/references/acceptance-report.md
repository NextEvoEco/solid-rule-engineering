# Analysis report

Record the analysis mode, inspected revision or working tree, rule pack version, targets, requirement sources, relevant contracts, search scope, and evidence gaps. Separate observed repository facts from semantic inferences.

## Semantic mapping

Map the relevant chain before reporting SOLID decisions:

| Requirement or behavior | Acceptance criterion | Change driver | Capability or policy | Code symbol | Evidence |
| --- | --- | --- | --- | --- | --- |
| `<source reference>` | `<AC or observable result>` | `<business or technical driver>` | `<meaning>` | `path:line · symbol` | `<requirement, caller, test, or source>` |

## Rule decisions

Report compliance, actual impact, and remediation necessity separately. Use `none`, `optional`, `planned`, `before-change`, or `immediate` for necessity.

| Target | Rule | Decision | Evidence | Impact | Necessity | Recommendation or disposition |
| --- | --- | --- | --- | --- | --- | --- |
| `path:line · symbol` | `SRP-F01` | `pass` | `<cited evidence>` | `none` | `none` | `<reasoned disposition>` |

For `uncertain`, identify the missing evidence and where to obtain it. For `accepted-exception`, include the authorization, scope, rationale, and any expiry. A failure does not by itself justify refactoring.

## Optional technical observations

Record read-only checks used to substantiate findings, including the command or inspection, result, and any unavailable or unrun checks. Do not add or modify tests, code, configuration, requirements, or other project artifacts.

## Completion gates

| Gate | Completion criteria |
| --- | --- |
| Scope | Requested targets, requirement sources, applicable rules, and search boundaries are recorded. |
| Semantic evidence | Relevant requirements or observable behavior, acceptance criteria, change drivers, and code symbols are mapped, or material gaps are explicit. |
| Rule analysis | Each applicable rule has a supported decision; warnings and exceptions have a disposition. |
| Recommendation | Compliance, actual impact, and remediation necessity are distinct; every recommendation cites a semantic or dependency reason and states material trade-offs. |
| Read-only contract | No code, tests, requirements, configuration, or other project artifacts were modified. |

Declare design conclusions provisional when implementation evidence is unavailable. An incomplete gate must name the concrete finding or missing evidence that prevents completion.
