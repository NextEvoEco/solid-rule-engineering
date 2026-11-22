# Function and method SRP rules

Rule pack version **0.2.0**. Apply only the rules relevant to the requested function or method analysis. The entries below are compact runtime projections of governed rules; their category structure follows the [Rule Markdown schema](rule-schema.md).

## SRP-F01 · MUST establish one observable purpose

- **Rule:** State one purpose as a verb, domain object, and observable result; map every major operation and effect to it.
- **Applies when:** Evaluating a function or method, including orchestration and adapters.
- **Requires:** Signature, body, return and error paths, side effects, and relevant requirements, callers, or tests.
- **Evaluate:** Pass when every major operation supports the stated purpose. Warn when the relationship is obscured but a second outcome is unproven. Fail when an operation supplies an independently required outcome outside that purpose. Use `uncertain` when the intended outcome or an operation's role is materially ambiguous.
- **On match:** Report the mapping and any separate outcome. Do not split cohesive coordination without evidence of a separate responsibility.
- **Exception:** Record an authorized framework-mandated entry point if it genuinely violates the rule.

## SRP-F02 · MUST identify independent change drivers

- **Rule:** Map directly implemented policies to requirements, acceptance criteria, or other evidenced change drivers before judging responsibility.
- **Applies when:** A target contains multiple operation groups, policies, or observable effects.
- **Requires:** Operation groups, requirements or observable contracts, callers, tests, and known ownership or change history when available.
- **Evaluate:** Pass when the drivers concern one cohesive policy or the target only coordinates delegates under one contract. Warn when a second driver is plausible but weakly supported. Fail when two independent policy changes would edit separate groups in the same target. Use `uncertain` when missing domain ownership or requirements could change the result.
- **On match:** Report the drivers, the evidence for their independence, actual impact, and whether remediation is necessary.
- **Exception:** Record an authorized atomicity or compatibility constraint; do not treat it as implicit approval.

## SRP-F03 · MUST relate dependencies to the purpose

- **Rule:** Account for each collaborator, global, external I/O operation, and external state access in relation to the target's stated purpose or required coordination.
- **Applies when:** The target uses a dependency or crosses a state or I/O boundary.
- **Requires:** Dependency inventory, uses, supported operations, and available contracts or tests.
- **Evaluate:** Pass when every dependency supports the outcome or its required coordination. Warn when a dependency exposes unnecessarily broad capability or avoidable coupling. Fail when a dependency serves an independent purpose outside the contract. Use `uncertain` when opaque dependency behavior is material.
- **On match:** Report unrelated or overly broad coupling and a proportional boundary recommendation.
- **Exception:** Record an authorized framework or generated-code constraint.

## SRP-F04 · MUST verify a consistent caller contract

- **Rule:** Compare how known callers depend on the target's inputs, output, side effects, errors, and mode-dependent branches.
- **Applies when:** The target has known callers, wrappers, registrations, or an intended contract for an uncalled internal target.
- **Requires:** Direct callers, relevant upstream wrappers, tests, branches, and recorded search scope.
- **Evaluate:** Pass when known uses preserve one core contract and visibility is sufficient. Warn when partial consumption or flags suggest a split but still serve one purpose. Fail when callers induce independently required behaviors that change responsibility. Use `uncertain` when hidden or external callers could change the conclusion.
- **On match:** Report the distinct caller contracts and any compatibility obligation.
- **Exception:** Record an authorized temporary compatibility requirement.

## SRP-F05 · MUST compare meaning before sharing logic

- **Rule:** Compare purpose, inputs, outputs, errors, side effects, and change drivers before recommending or accepting shared logic.
- **Applies when:** Similar code exists or an extraction is proposed.
- **Requires:** A scoped search by symbols, domain terms, and distinctive operations plus representative candidate locations.
- **Evaluate:** Pass when candidate treatment matches the semantic evidence or no material candidate is found. Warn when a common contract is supported and duplication presents a concrete drift risk. Fail when sharing forces unrelated contracts or change drivers into one implementation. Use `uncertain` when candidate behavior or ownership is unavailable.
- **On match:** Recommend sharing only a stable common operation whose meaning aligns; otherwise retain independent implementations.
- **Exception:** Record an authorized temporary compatibility constraint.

## SRP-F06 · MUST NOT infer responsibility from structural counts alone

- **Rule:** Do not determine an SRP violation solely from line count, parameter count, branch count, dependency count, method count, or caller count.
- **Applies when:** A structural metric or size heuristic is used in an SRP rationale.
- **Requires:** The rationale and the semantic evidence used with the metric.
- **Evaluate:** Pass when counts only prioritize inspection and the decision rests on requirements, observable behavior, caller contracts, and change drivers. Fail when a count is the sole basis. Use `uncertain` when the semantic evidence has not been collected.
- **On match:** Reject the count-only rationale and request or collect semantic evidence.

## SRP-F07 · MUST NOT turn a violation into automatic remediation

- **Rule:** Do not recommend refactoring solely because an SRP rule fails; assess actual impact, change likelihood, scope, correction cost, and correction risk.
- **Applies when:** A target has a `fail` or material `warning` decision.
- **Requires:** The finding, current pain or risk, known change demand, affected scope, and available correction options.
- **Evaluate:** Pass when compliance, impact, and remediation necessity are reported separately. Fail when the finding is presented as an unconditional instruction to split or abstract.
- **On match:** Replace the automatic prescription with `none`, `optional`, `planned`, `before-change`, or `immediate` necessity and explain the basis.
