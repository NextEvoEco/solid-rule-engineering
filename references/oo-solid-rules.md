# Object-oriented SOLID rules

Rule pack version **0.2.0**. These are compact LLM runtime projections. Apply only rules whose target and applicability match the task. Use the [Rule Markdown schema](rule-schema.md) for governed authoring records and the [function and method SRP rules](srp-function-rules.md) when method-level detail is material.

## Semantic basis

### SEM-P01 · MUST establish requirement semantics

- **Rule:** Identify the business capability, observable outcomes, acceptance criteria, policies, consistency needs, data needs, external effects, and known change drivers relevant to the target.
- **Applies when:** Performing any SOLID analysis.
- **Requires:** Requirements or, when unavailable, observable behavior supported by callers, tests, contracts, and source evidence.
- **Evaluate:** Pass when the semantic basis is cited and facts are separated from inference. Use `uncertain` when missing semantics could change a finding.
- **On match:** Use the semantic basis for all later rule decisions.

### SEM-P02 · MUST map semantics to implementation units

- **Rule:** Map relevant requirements, acceptance criteria, policies, and change drivers to packages, classes, interfaces, and methods before recommending a boundary change.
- **Applies when:** Code or a proposed OO design is available.
- **Requires:** The semantic basis and target symbols with relevant callers and dependencies.
- **Evaluate:** Pass when each finding is traceable in both directions or a material gap is explicit. Fail when a recommendation relies only on code shape.
- **On match:** Report the mapping and evidence gaps.

### SEM-C01 · MUST NOT confuse roles with mandatory structures

- **Rule:** Do not require a service, DAO, repository, adapter, transaction, interface, hierarchy, or design pattern merely because its role can be named.
- **Applies when:** Classifying business logic, data access, external effects, or consistency needs.
- **Requires:** A demonstrated semantic, substitution, dependency, persistence, or atomicity need.
- **Evaluate:** Pass when a proposed structure answers a present need. Fail when the role name is the sole justification.
- **On match:** Retain the semantic classification but reject the unsupported structure.

## Single Responsibility Principle

### SRP-P01 · MUST align a package with cohesive change drivers

- **Rule:** Group packages or modules around cohesive capabilities and change drivers; identify unrelated business policies that force independent changes through the same package boundary.
- **Applies when:** Reviewing a package, module, namespace, or feature boundary.
- **Requires:** Package public API, dependencies, contained responsibilities, supported requirements, and change drivers.
- **Evaluate:** Pass when the boundary contains a cohesive capability or intentionally shared stable foundation. Warn when ownership is unclear. Fail when unrelated policies are coupled through the same public boundary and change independently.
- **On match:** Report the coupled capabilities and their observed change relationship.

### SRP-C01 · MUST distinguish policy from orchestration

- **Rule:** Determine whether a class directly implements independently changing policies or cohesively coordinates delegates for one use-case contract.
- **Applies when:** Reviewing a class, service, controller, coordinator, entity, repository, DAO, or adapter.
- **Requires:** Public behaviors, requirements or observable contracts, collaborators, callers, and change drivers.
- **Evaluate:** Pass when directly implemented behavior has one cohesive change basis or the class only coordinates one outcome. Fail when it directly implements independent policies that change for different reasons. Use `uncertain` when ownership or semantics are missing.
- **On match:** Preserve cohesive orchestration; identify only the independently changing policy boundaries.

### SRP-M01 · MUST evaluate method responsibility semantically

- **Rule:** Apply the detailed function and method SRP rules to observable purpose, change drivers, dependencies, caller contracts, and candidate sharing.
- **Applies when:** Method-level analysis is requested or necessary to support a class finding.
- **Requires:** Load only the applicable entries from [the method rule pack](srp-function-rules.md).
- **Evaluate:** Use the decisions and evidence requirements in the selected method rules.
- **On match:** Report the selected rule IDs rather than loading or repeating unrelated method rules.

### SRP-C02 · MUST NOT infer responsibility from size or counts

- **Rule:** Do not infer responsibility count solely from lines, methods, branches, parameters, dependencies, callers, files, or folders.
- **Applies when:** A structural metric appears in an SRP rationale.
- **Requires:** Requirement semantics, observable behavior, and change-driver evidence.
- **Evaluate:** Pass when metrics only prioritize inspection. Fail when a metric is the semantic conclusion.
- **On match:** Reject the count-only rationale.

## Open/Closed Principle

### OCP-C01 · MUST demonstrate a variation axis before abstraction

- **Rule:** Identify an observed or concretely committed variation whose additions repeatedly modify a stable policy before recommending an extension boundary.
- **Applies when:** A conditional, provider set, type branch, plugin point, or proposed abstraction is under review.
- **Requires:** Existing variants, change history or committed requirements, common contract, and modification risk.
- **Evaluate:** Pass when treatment matches the demonstrated variation. Warn when variation is plausible but weakly evidenced. Fail when a growing variation repeatedly changes stable policy without a justified boundary.
- **On match:** Recommend the simplest extension mechanism that absorbs the demonstrated change.

### OCP-C02 · MUST NOT create speculative extension points

- **Rule:** Do not recommend an interface, strategy, factory, registry, plugin system, or hierarchy for hypothetical variation alone.
- **Applies when:** An extension abstraction is proposed.
- **Requires:** Present variants or a concrete accepted requirement for variation.
- **Evaluate:** Pass when present evidence justifies the abstraction. Fail when speculation is the sole basis.
- **On match:** Reject the premature abstraction and record what future evidence would justify it.

## Liskov Substitution Principle

### LSP-I01 · MUST preserve substitutable behavior

- **Rule:** Verify that each subtype or implementation preserves the shared contract's accepted inputs, outputs, errors, side effects, state invariants, and relevant temporal behavior.
- **Applies when:** A base type, interface, protocol, or substitutable implementation exists.
- **Requires:** Shared contract, implementation behavior, consumer expectations, and contract tests when available.
- **Evaluate:** Pass when consumers can substitute implementations without special knowledge. Warn when the contract is incomplete. Fail when an implementation strengthens preconditions, weakens postconditions, violates invariants, or requires consumer type checks.
- **On match:** Report the incompatible behavior and affected consumers.

### LSP-C01 · MUST NOT assume substitutability from type conformance

- **Rule:** Do not declare LSP compliance solely because code compiles or a class implements an interface.
- **Applies when:** Static type conformance is used as evidence.
- **Requires:** Behavioral contract and consumer evidence.
- **Evaluate:** Pass when behavior supports conformance. Fail when type conformance is the sole rationale.
- **On match:** Request or inspect behavioral evidence.

## Interface Segregation Principle

### ISP-I01 · MUST evaluate interfaces by consumer needs

- **Rule:** Compare which interface operations each consumer requires and whether consumers or implementations depend on irrelevant capabilities.
- **Applies when:** Reviewing an interface, protocol, public facade, context, store, or package API.
- **Requires:** Consumer-operation usage, implementation obligations, change patterns, and runtime coupling when relevant.
- **Evaluate:** Pass when the interface represents a cohesive consumer contract. Warn when usage is unclear. Fail when consumers are forced to depend on unrelated operations or implementations must provide unsupported behavior.
- **On match:** Recommend the smallest cohesive consumer-aligned boundary, not the greatest number of interfaces.

### ISP-C01 · MUST NOT infer violation from interface size alone

- **Rule:** Do not judge ISP solely by method or property count.
- **Applies when:** Interface size is cited as the rationale.
- **Requires:** Consumer usage and change-driver evidence.
- **Evaluate:** Pass when size only prompts inspection. Fail when size alone determines the finding.
- **On match:** Reject the count-only rationale.

## Dependency Inversion Principle

### DIP-P01 · MUST identify policy and detail boundaries

- **Rule:** Determine whether stable business policy depends directly on volatile infrastructure, framework, vendor, storage, transport, or UI details that can change independently.
- **Applies when:** Reviewing dependencies across packages, classes, or integration boundaries.
- **Requires:** Dependency direction, policy ownership, detail volatility, callers, and test or replacement needs.
- **Evaluate:** Pass when dependency direction protects the stable policy or direct dependency is proportionate and harmless. Warn when volatility is plausible but unproven. Fail when independent technical change penetrates and modifies stable policy.
- **On match:** Recommend the narrowest consumer-owned boundary that addresses the demonstrated coupling.

### DIP-C01 · MUST NOT require one interface per class

- **Rule:** Do not recommend an abstraction solely to mirror a concrete class or satisfy a diagrammatic layer pattern.
- **Applies when:** Introducing an interface or port.
- **Requires:** A demonstrated policy boundary, substitution need, test isolation need, or independent dependency lifecycle.
- **Evaluate:** Pass when the abstraction has a present consumer-owned purpose. Fail when mirroring is the sole purpose.
- **On match:** Reject the redundant abstraction.

## Recommendation proportionality

### REC-P01 · MUST separate compliance, impact, and necessity

- **Rule:** Report rule compliance, actual impact, and remediation necessity as separate conclusions.
- **Applies when:** Reporting any failure or material warning.
- **Requires:** Current pain or risk, expected change likelihood, affected scope, correction cost, and correction risk when known.
- **Evaluate:** Pass when necessity is one of `none`, `optional`, `planned`, `before-change`, or `immediate` with evidence. Fail when a violation is treated as an automatic refactoring instruction.
- **On match:** Give a proportional recommendation, alternatives, and trade-offs.
