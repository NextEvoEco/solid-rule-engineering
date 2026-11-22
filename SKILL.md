---
name: solid-rule-engineering
description: Analyze object-oriented requirements and code with evidence-based SOLID rules without modifying the implementation. Use when Codex must map requirements, acceptance criteria, business semantics, and change drivers to packages, classes, interfaces, or methods; review responsibility and dependency boundaries; assess the impact of a business change; or produce proportional SOLID findings and recommendations.
---

# SOLID Rule Engineering

## Identity

- **Stable key:** `solid-rule-engineering`
- **Type:** work
- **Mode:** read-only analysis, review, and recommendation
- **Rule pack:** object-oriented SOLID `0.2.0`

## Context

### Purpose

Relate requirement semantics to code structure before applying SOLID. Treat packages, classes, interfaces, and methods as implementation units; treat service, DAO, repository, adapter, and transaction as roles or relationships inferred from the requirements, not mandatory shapes.

### Application timing

Apply this skill when the task concerns:

- requirement-to-code mapping;
- responsibility or dependency review;
- SOLID assessment of object-oriented code;
- package, class, interface, or method boundary recommendations; or
- the effect of a business requirement change on existing code and tests.

### Required context

Collect only the context material to the requested scope:

- requirements, acceptance criteria, constraints, and known change drivers;
- target packages, classes, interfaces, methods, and their contracts;
- relevant callers, tests, dependencies, data operations, and external effects; and
- visibility gaps such as unavailable requirements, external callers, dynamic dispatch, or framework bindings.

Use repository behavior, callers, and tests as evidence when formal requirements are unavailable. Label inferred business meaning as inference, not fact.

### Analysis guidance

1. Identify the requested mode, scope, targets, and available requirement evidence.
2. Extract the business capability, observable outcomes, acceptance criteria, policies, consistency needs, data needs, and external effects relevant to the target.
3. Map those semantics and their change drivers to the implementation units. Distinguish policy implementation from cohesive orchestration.
4. Load the [rule schema](references/rule-schema.md) and only the applicable runtime projections from the [OO SOLID rule pack](references/oo-solid-rules.md). Load the [function and method SRP rules](references/srp-function-rules.md) only when method-level detail is material.
5. Evaluate compliance, actual impact, and remediation necessity separately.
6. Produce the report using the [acceptance report](references/acceptance-report.md).

## Contract

### MUST

- MUST establish the requirement or observable-behavior basis before making a SOLID finding.
- MUST map each finding to requirements, acceptance criteria, callers, tests, source locations, or an explicitly labeled inference.
- MUST identify independent change drivers before recommending a responsibility split or abstraction.
- MUST select rules by target level and applicability instead of loading the complete rule catalog into the analysis.
- MUST preserve the distinction between a business capability, an implementation unit, a technical role, and a consistency boundary.
- MUST use `uncertain` when missing or ambiguous evidence could change the decision.
- MUST assess rule compliance, actual impact, and remediation necessity as separate conclusions.
- MUST state the inspected scope, rule pack version, evidence gaps, and applicable rule IDs.

### MUST NOT

- MUST NOT modify code, tests, requirements, configuration, or other project artifacts.
- MUST NOT invent undocumented requirements, constraints, ownership, or change drivers.
- MUST NOT infer responsibility count solely from line count, method count, branch count, dependency count, or syntax.
- MUST NOT split cohesive orchestration merely because it coordinates multiple operations.
- MUST NOT recommend shared logic solely because implementations are syntactically similar.
- MUST NOT recommend an interface, hierarchy, service, DAO, repository, or design pattern without a demonstrated semantic or dependency need.
- MUST NOT present a rule failure as an automatic instruction to refactor.

### Expected output

Report, as applicable:

- scope and evidence inventory;
- requirement, acceptance-criteria, change-driver, and code-symbol mapping;
- per-rule decision and cited evidence;
- repository facts separated from semantic inferences;
- actual impact and remediation necessity;
- proportional recommendation, alternatives, and trade-offs; and
- uncertainties, accepted exceptions, and missing evidence.

### Completion criteria

Complete the analysis only when every requested target and applicable rule has a supported decision or an explicit evidence gap, each recommendation names the semantic reason it is warranted, and no prohibited modification was made.
