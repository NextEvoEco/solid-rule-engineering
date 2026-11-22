# solid-rule-engineering

Evidence-based, read-only SOLID analysis that starts from **requirements**, not code.

## Concept

Most SOLID tools start from code and apply principles as pattern-matching rules.
This skill works the other way: it derives SOLID findings from requirement semantics
and traces them back to acceptance criteria, change drivers, and business rules.

```
Requirements / AC / Change drivers
        ↓
Map to packages, classes, interfaces, methods
        ↓
Apply only the SOLID rules relevant to the target
        ↓
Report compliance · impact · remediation necessity separately
        ↓
Evidence-cited recommendations — no automatic refactoring
```

The key distinction is **defensibility**: a finding is not "this method looks long"
but "SRS §3.2 and §5.1 have independent change drivers that map to separate
operation groups in the same method."

### Three modes

| Mode           | When to use           | Input                                          |
| -------------- | --------------------- | ---------------------------------------------- |
| **Design**     | Before implementation | PRD, SRS, STS, user stories, or a plain prompt |
| **Review**     | During implementation | Partial code, current diff                     |
| **Acceptance** | After implementation  | Complete code, callers, tests, diff            |

### When requirements are unavailable

The skill degrades gracefully. When no formal documents exist, it uses observable
behavior — callers, tests, contracts, and source code — as evidence. Findings
derived from inferred semantics are labeled as inference, not fact, and are reported
as `uncertain` rather than `fail` when missing context could change the decision.

### AI-generated and AI-maintained code

When AI generates code, it optimizes for local coherence — clean structure, DRY
patterns, readable names. When AI later maintains that code, the same tendency
becomes a risk: it may merge functions that look similar but have independent
change drivers, or refactor away a boundary that was deliberately placed for a
business reason it cannot see.

This is **semantic erosion**: the code still works, but the business boundaries
quietly disappear.

Requirements-driven analysis produces artifacts that resist this. A traceability
table that records `completePayment → SRS §3.2 + AC-002, independent of §5.1`
tells the next AI agent which boundaries have a documented reason and must not be
"optimized" away. A finding marked `uncertain` tells it the evidence was
incomplete — verify before changing.

The analysis report and requirement–code map committed to the repository become
**LLM-readable maintenance contracts**: structured evidence that future agents
can load as context before modifying any code they did not write.

```
AI generates code with SOLID boundaries
        ↓
Skill produces semantic mapping + change-driver evidence
        ↓
Artifacts committed to the repository
        ↓
AI maintenance agent loads artifacts as context
        ↓
Boundaries with documented reasons survive refactoring
        ↓
Next analysis has richer evidence to work with
```

### What the skill will not do

- Modify code, tests, requirements, or any project artifact
- Recommend an abstraction, interface, or design pattern without a demonstrated semantic need
- Split cohesive orchestration merely because it coordinates multiple operations
- Present a rule failure as an automatic instruction to refactor

---

## Usage

### Codex

```sh
codex skill install .
```

Invoke with a target and a task:

```text
Use $solid-rule-engineering to review OrderPaymentService for SRP and DIP.
Map the change drivers from SRS §4 to the method responsibilities.
```

Design mode before implementation:

```text
Use $solid-rule-engineering in design mode.

Requirement: when an order is paid, record the payment, update inventory,
send a receipt, and notify the warehouse.

Identify responsibility boundaries and propose function-level design.
State assumptions and unresolved requirements. Do not write code.
```

### Claude Code

Install via the plugin manifest:

```sh
cp -r platforms/claude-code/.  <your-project>/.claude-plugin/solid-rule-engineering/
```

Then invoke in a task:

```text
Use $solid-rule-engineering to review src/checkout/ for OCP.
```

### Copilot

Copilot reads `.github/copilot-instructions.md`. Generate a flat file from
the canonical sources:

```powershell
@(
  Get-Content SKILL.md
  "`n---`n"
  Get-Content references/rule-schema.md
  "`n---`n"
  Get-Content references/oo-solid-rules.md
  "`n---`n"
  Get-Content references/srp-function-rules.md
  "`n---`n"
  Get-Content references/acceptance-report.md
) | Set-Content .github/copilot-instructions.md -Encoding utf8
```

See [`platforms/copilot/install.md`](platforms/copilot/install.md) for details.

### OpenAI Agent

The skill is registered in [`agents/openai.yaml`](agents/openai.yaml).
Point your agent configuration at that file or reference it in your agent manifest.

---

## Repository layout

```
SKILL.md                      Canonical skill contract
agents/openai.yaml            OpenAI Agent manifest
references/
  rule-schema.md              Rule authoring and runtime projection schema
  oo-solid-rules.md           OO SOLID runtime rule pack (SEM, SRP, OCP, LSP, ISP, DIP, REC)
  srp-function-rules.md       Function and method SRP rules
  acceptance-report.md        Analysis report structure
examples/
  srp-function-review.md      End-to-end example review
evals/
  cases.json                  Regression cases for Skill validation
  fixtures/                   Input fixtures for eval cases
templates/
  analysis-report.md          Blank analysis report
  requirement-code-map.md     Requirement–code traceability matrix
  rule-authoring.md           Rule authoring template
platforms/
  claude-code/plugin.json     Claude Code plugin manifest
  codex/install.md            Codex installation
  copilot/install.md          Copilot flat-file generation
  opencode/install.md         OpenCode configuration
```

---

## Rule pack 0.2.0

Covers semantic-first OO SOLID analysis at package, class, interface, and method levels.

| Prefix | Principle                                                  |
| ------ | ---------------------------------------------------------- |
| `SEM`  | Semantic basis — requirement mapping before any SOLID rule |
| `SRP`  | Single Responsibility Principle                            |
| `OCP`  | Open/Closed Principle                                      |
| `LSP`  | Liskov Substitution Principle                              |
| `ISP`  | Interface Segregation Principle                            |
| `DIP`  | Dependency Inversion Principle                             |
| `REC`  | Recommendation proportionality                             |
