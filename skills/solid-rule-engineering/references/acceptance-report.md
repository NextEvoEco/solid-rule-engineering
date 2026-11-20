# Acceptance report

Record the task mode, reviewed revision or working tree, rule pack version, target symbols, relevant contracts, and evidence scope. For each target, report each rule's ID, status, evidence locations, rationale, and any correction, uncertainty, or warning disposition. For an accepted exception, include its authorization and scope.

| Target | Rule | Status | Evidence | Rationale and disposition |
| --- | --- | --- | --- | --- |
| `path:line · symbol` | `SRP-F01` | `pass` | Source, caller, contract, or test | Explain how the evidence meets the condition. |

Report technical checks separately with the command, result, and any skipped, unavailable, or unrun checks. Cite the difference between observed repository facts and inferred domain intent where it affects a decision.

## Completion gates

| Gate | Completion criteria |
| --- | --- |
| Analysis | Targets and applicable rules are accounted for. Each decision cites evidence or specifies a material gap. |
| Implementation | When requested, the final change meets the agreed responsibility boundaries and preserves external contracts except for authorized behavior changes. For review or design, mark this gate out of scope. |
| Technical verification | The checks required for the requested workflow ran successfully. List skipped or unavailable checks and mark the gate incomplete if a required check could not run. If the requested scope calls for no technical checks, explain why. |
| Rule acceptance | Each applicable blocking rule passes or has an accepted exception. There are no unresolved failures or uncertain decisions on applicable rules. Each warning has a disposition. Modified targets and affected callers have been re-evaluated using final evidence. |

Declare review findings for the inspected revision, design conclusions as provisional, and implementation acceptance only after all applicable gates are complete. An incomplete gate needs the concrete finding or missing evidence that prevents completion.
