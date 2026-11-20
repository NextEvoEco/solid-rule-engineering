# Function and method SRP rules

Rule pack version **0.1.0**. Each rule applies to functions and methods, including orchestration and adapters.

## SRP-F01 · Single observable purpose

- **Objective and severity.** Establish one observable outcome. Blocking.
- **Context and checks.** Inspect the signature, body, return and error paths, documented contract, and relevant callers or tests. Inventory the major operations and observable effects. Write one purpose using a verb, domain object, and result. Map each operation group to that purpose.
- **Evidence and completion.** Cite the target and each major operation group, with evidence for the expected outcome and any group that serves a separate outcome.
- **Decision.** Pass when every major operation supports the stated purpose. Warn when the implementation obscures the relationship but a separate outcome is unproven. Fail when a major operation delivers an independently required outcome outside the stated purpose. Use uncertain when the intended outcome or an operation's role could change the finding.
- **Exceptions, correction, and recheck.** A framework-mandated entry point may qualify with documented approval if it genuinely violates the rule. Prefer extracting the separate outcome while keeping cohesive coordination. Re-map the operations and exercise observable behavior.

## SRP-F02 · One reason to change

- **Objective and severity.** Keep independently changing policies out of the same implementation boundary. Blocking.
- **Context and checks.** Inspect requirements, operation groups, contracts, tests, and relevant callers. Map each group to its change driver. Compare concrete changes and determine whether they would modify unrelated policy in the same function.
- **Evidence and completion.** Cite each group and a requirement, caller, test, or source behavior that supports each change driver. Describe what would change and where.
- **Decision.** Pass when identified drivers concern a single policy or the function only coordinates delegates under one contract. Warn when another driver is plausible with weak evidence. Fail when two independent policy changes would require edits to separate groups in the same function. Use uncertain when domain ownership or the change drivers are indeterminate and could change the decision.
- **Exceptions, correction, and recheck.** An approved atomicity requirement may justify keeping a violation together. Otherwise move independently changing policy into focused functions while preserving ordering and atomicity. Repeat the change-driver analysis on the caller and each extracted function.

## SRP-F03 · Dependencies support the purpose

- **Objective and severity.** Keep dependencies relevant to the function's outcome. Blocking.
- **Context and checks.** Inventory parameters used as collaborators, injected and direct dependencies, globals, external I/O, and external state read or written. Trace how each supports the purpose and which technical or domain detail the function owns.
- **Evidence and completion.** Cite the dependency and its use, the supported operation, and any coupling to unrelated behavior.
- **Decision.** Pass when every dependency serves the outcome or its required coordination. Warn when a relevant dependency exposes a broader capability than the function needs or creates avoidable coupling. Fail when a dependency serves an independent purpose outside the function's contract. Use uncertain when a dependency's behavior or usage is opaque and material.
- **Exceptions, correction, and recheck.** An approved framework or generated-code constraint may justify a specific violation. Move unrelated dependencies with their behavior. Recheck dependency use and run affected interactions through tests or the available verification path.

## SRP-F04 · Consistent contract across callers

- **Objective and severity.** Preserve one core contract across consumers. Blocking.
- **Context and checks.** Find direct callers and follow relevant wrappers, registrations, and upstream calls. Check how each purpose maps to the function's inputs, output, side effects, and errors. Inspect flags and identity-based branches for changes to the responsibility.
- **Evidence and completion.** Cite callers, how they consume the function, the searched scope, and relevant branches or tests. An internal target with no current callers can pass with adequate evidence of its intended contract and covered paths. Treat material hidden or external callers as unknown.
- **Decision.** Pass when known uses and branches preserve the core contract and visibility is sufficient. Warn when partial consumption or mode flags suggest a split but serve the same purpose. Fail when consumers induce independently required behaviors that change the responsibility of the function. Use uncertain when an unresolved caller or contract could alter the conclusion. Caller count only indicates search scope.
- **Exceptions, correction, and recheck.** A documented and approved compatibility obligation may justify temporary mixed behavior. Preserve existing entry points as needed and delegate distinct behaviors to focused functions. Revisit callers and exercise each affected contract.

## SRP-F05 · Share logic only when its meaning aligns

- **Objective and severity.** Evaluate similar implementations before extraction. Advisory.
- **Context and checks.** Search the target area by names, domain terms, and distinctive operations. Compare candidates' purpose, inputs, outputs, errors, side effects, and change drivers. Inspect any shared implementation introduced by the diff.
- **Evidence and completion.** Record search scope and representative queries, cite candidate locations, and document the shared or independent contract and why extraction is or is not warranted.
- **Decision.** Pass when a scoped search identifies no material candidate, or candidate treatment matches the semantic evidence. Warn when a common contract is supported and duplication carries a concrete risk of drift. Fail when an existing or proposed extraction forces unrelated contracts or change drivers into one implementation. Use uncertain when material candidate behavior or ownership is unavailable.
- **Exceptions, correction, and recheck.** An authorized compatibility constraint may permit a conflicting shared implementation temporarily. Keep independent semantics separate. Extract a stable common operation only if the observed contracts align. Repeat the search and verify each affected contract after any change.
