# RULE-ID · title

## Identification

- **Category:** [catalog category]
- **Version:** 0.1.0
- **Level:** `MUST` | `MUST NOT`
- **Status:** `draft`
- **Source:** [source identifier]

## Statement

[One atomic obligation or prohibition.]

## Intent

- **Reason:** [why the rule exists]
- **Objectives:** [one or more protected outcomes]

## Context

- **Target:** [package, class, interface, method, or other artifact]
- **Applies when:** [applicability conditions]
- **Required context:** [evidence needed before applying the rule]
- **Does not apply when:** [inapplicability conditions]

## Evaluation

- **Procedure:** [observable analysis steps]
- **Decision:**
  - `pass`: [condition]
  - `warning`: [condition]
  - `fail`: [condition]
  - `uncertain`: [condition — missing evidence that could change the result]
  - `not-applicable`: [condition]
- **On match:** [continue, stop, reject rationale, or report]
- **Exceptions:** [authorized exception conditions]

## Responsibility

- **AI:** [AI responsibility]
- **Human:** [human responsibility]

## Governance

- **Risk:** `low` | `medium` | `high` | `critical`
- **Severity:** `low` | `medium` | `high` | `critical`
- **Acceptance effect:** `blocking` | `advisory`

## Verification

- **Outcome:** [observable compliant result]
- **Evidence:** [required evidence]
- **Audit:** [audit method]
- **Recheck:** [how to re-evaluate after a change]

---

## LLM runtime projection

```markdown
### RULE-ID · MUST | MUST NOT

- **Rule:** [atomic statement]
- **Applies when:** [current applicability]
- **Requires:** [minimum evidence]
- **Evaluate:** [compact procedure and decision conditions]
- **On match:** [runtime action]
- **Exception:** [only when relevant]
```
