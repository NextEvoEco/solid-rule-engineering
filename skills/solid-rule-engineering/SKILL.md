---
name: solid-rule-engineering
description: Apply evidence-based Single Responsibility Principle (SRP) rules to functions and methods when designing, generating, reviewing, or refactoring code. Use when asked to assess a function's purpose, reasons to change, dependencies, caller behavior, or whether similar implementations should share logic, or to produce a SOLID acceptance report for function-level changes.
---

# SOLID Rule Engineering

Use the [rule schema](references/rule-schema.md), the [SRP function rules](references/srp-function-rules.md), and the [acceptance report](references/acceptance-report.md). The v0.1.0 rule pack covers function- and method-level SRP. State the scope and rule pack version in the report.

## 1. Analyze the scope

1. Identify the requested mode (review, design, implementation, or refactor), target symbols, expected behavior, and any authorized contract changes. Review and design requests produce findings or a proposed design. Implementation and refactor requests may modify code.
2. Inspect the signature, body, contracts, tests, direct dependencies, and callers. Follow upstream calls where they clarify which contract callers rely on. Search by symbol and by related domain behavior for similar implementations. For new code, use the proposed API, known integration points, and nearby implementations as design inputs.
3. Record search scope, tool observations, and visibility gaps such as dynamic dispatch, framework bindings, external callers, or unavailable tests. Separate repository facts from semantic inferences. Use path and line references or named test assertions for evidence.
4. Evaluate SRP-F01 through SRP-F05 per target. Explain inapplicability or missing context. In a design-only task, label results provisional and identify the evidence still needed from implementation.

## 2. Implement when requested

- State each changed function's purpose, inputs, outputs, side effects, and error behavior. Use the simplest boundary that addresses the confirmed reasons to change.
- Preserve caller-observable behavior and required transaction ordering unless the request authorizes a change. Retain cohesive orchestration when each step serves its stated outcome.
- Extract shared behavior only when the contracts and reasons to change align. Introduce abstractions when a demonstrated variation or dependency boundary warrants them.
- Address supported findings within scope. Record unresolved findings and where they occur.

## 3. Verify the final code

Run the applicable repository build, type checks, static analysis, and focused tests. Use existing tests where they exercise the changed behavior and add coverage when needed to demonstrate the changed contract. Record the command, outcome, and checks that could not be run. For a review, record the checks used to substantiate the findings and any checks outside the requested scope.

Re-read the final diff and re-evaluate all five rules on the changed targets and affected callers, including newly extracted functions. Use final source locations and test results. Keep technical verification and rule acceptance separate in the report. Use the [gate criteria](references/acceptance-report.md#completion-gates) to decide whether acceptance is complete.
