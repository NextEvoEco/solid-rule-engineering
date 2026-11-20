# Rule schema

Use a stable ID for each rule and version the rule pack independently of the skill. Record the evaluated pack version in each report. When changing a rule, keep its ID for revisions to the same requirement. Assign a new ID when introducing a separate requirement.

Each rule declares its ID, title, objective, scope, severity, required context, observable checks, semantic procedure, required evidence, decision conditions, completion criteria, exceptions, remediation, and recheck method.

## Decisions

| Status | Evidence needed |
| --- | --- |
| `pass` | Required context is sufficient and the cited evidence meets the rule's pass conditions. |
| `warning` | Evidence shows a specific risk or weak signal, but falls short of the fail condition. Record a disposition. |
| `fail` | Evidence demonstrates a fail condition. Cite the counterexample and identify a behavior-preserving correction where possible. |
| `uncertain` | Missing or ambiguous evidence could change the result. Identify what and where to check next. |
| `not-applicable` | The target is outside the rule's scope or the rule defines an applicability condition that is absent. Cite the basis. |
| `accepted-exception` | A demonstrated violation has documented approval from the user or an authorized repository owner or policy. Record the source, scope, rationale, and any expiry. |

For an applicable rule, a demonstrated violation takes precedence over missing context elsewhere. If no violation is established and the missing context could change the decision, use `uncertain`. A candidate exception remains `fail` until its approval is evidenced. Preserve the underlying evidence when recording an approved exception.

`blocking` rules require a supported pass or accepted exception when applicable. `advisory` rules guide remediation. Unresolved failures of either severity prevent full acceptance. Counts of lines, parameters, branches, collaborators, and callers help prioritize inspection. A decision requires evidence about behavior and domain intent. A search returning no results establishes only what was found within its recorded scope.
