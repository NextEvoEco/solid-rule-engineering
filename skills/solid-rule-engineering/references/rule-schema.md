# Rule Markdown schema

Use this authoring schema for governed rules. Keep the category headings stable. Keep common fields consistent, but add category-local fields when a rule has a distinct need. Do not send the complete authoring record to the LLM; compile the runtime projection described below.

## Authoring structure

```markdown
# <RULE-ID> · <title>

## Identification

- **Category:** <catalog category>
- **Version:** <semver>
- **Level:** `MUST` | `MUST NOT`
- **Status:** `draft` | `enabled`
- **Source:** <source identifier>

## Statement

<One atomic obligation or prohibition. Interpret MUST as 強制 and MUST NOT as 阻擋.>

## Intent

- **Reason:** <why the rule exists>
- **Objectives:** <one or more protected outcomes>
- **<custom field>:** <rule-specific intent>

## Context

- **Target:** <package, class, interface, method, or other artifact>
- **Applies when:** <applicability conditions>
- **Required context:** <evidence needed before applying the rule>
- **Does not apply when:** <inapplicability conditions>
- **<custom field>:** <rule-specific context>

## Evaluation

- **Procedure:** <observable analysis steps>
- **Decision:** <pass, warning, fail, uncertain, not-applicable, and accepted-exception conditions as needed>
- **On match:** <continue, stop, reject rationale, or report>
- **Exceptions:** <authorized exception conditions>
- **<custom field>:** <rule-specific evaluation>

## Responsibility

- **AI:** <AI responsibility>
- **Human:** <human responsibility>
- **<custom field>:** <other actor or system responsibility>

## Governance

- **Risk:** `low` | `medium` | `high` | `critical`
- **Severity:** `low` | `medium` | `high` | `critical`
- **Acceptance effect:** `blocking` | `advisory`
- **<custom field>:** <approval, expiry, priority, or policy>

## Verification

- **Outcome:** <observable compliant result>
- **Evidence:** <required evidence>
- **Audit:** <audit method>
- **Recheck:** <how to re-evaluate after a change>
- **<custom field>:** <rule-specific verification>
```

## Field semantics

- `MUST` is a positive obligation. The required action or result must occur.
- `MUST NOT` is a prohibition. A match blocks the prohibited action or rationale.
- Level does not express risk, severity, or acceptance effect; keep those in Governance.
- Keep each Statement atomic. Split multiple independent obligations or prohibitions into separate rule IDs.
- Use custom fields only inside an existing category. Do not create synonymous category names for individual rules.
- Preserve a rule ID when revising the same requirement. Assign a new ID for a separate requirement.
- Version the rule pack independently from the skill and report the evaluated version.

## Decisions

Rules that evaluate a target may use these decisions. A procedural rule may instead record whether its MUST or MUST NOT condition was satisfied.

| Decision | Required basis |
| --- | --- |
| `pass` | Required context is sufficient and the evidence satisfies the rule. |
| `warning` | Evidence shows a specific risk or weak signal but not a violation. |
| `fail` | Evidence demonstrates a violation. |
| `uncertain` | Missing or ambiguous evidence could change the decision. |
| `not-applicable` | The target or situation is outside the rule's applicability. |
| `accepted-exception` | A demonstrated violation has documented approval, scope, rationale, and any expiry. |

A candidate exception remains `fail` until approval is evidenced. Counts and syntax may prioritize inspection but do not establish semantic responsibility. A search with no result proves only what was found in the recorded scope.

## LLM runtime projection

Project only the fields needed for the current task. Omit Responsibility, maintenance metadata, and Governance unless they affect execution, conflict resolution, or the requested report.

```markdown
### <RULE-ID> · <MUST | MUST NOT>

- **Rule:** <atomic statement>
- **Applies when:** <current applicability>
- **Requires:** <minimum evidence>
- **Evaluate:** <compact procedure and decision conditions>
- **On match:** <runtime action>
- **Exception:** <only when relevant>
```

Select rules by task mode, target type, profile, and available evidence. Deduplicate common constraints at the skill contract level. Load examples or extended rationale only when they resolve an ambiguity. The runtime rule set must leave most of the context budget for requirements, code, callers, and tests.
