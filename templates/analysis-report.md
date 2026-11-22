# Analysis report — [target or scope]

**Mode:** `design` | `review` | `acceptance`  
**Rule pack:** 0.2.0  
**Revision or working tree:** [commit or branch]  
**Targets:** [package, class, interface, or method list]  
**Requirement sources:** [document references or "observable behavior only"]  
**Search scope:** [directories or files inspected]

---

## Semantic mapping

| Requirement or behavior | Acceptance criterion | Change driver | Capability or policy | Code symbol | Evidence |
| --- | --- | --- | --- | --- | --- |
| `<source reference>` | `<AC or observable result>` | `<business or technical driver>` | `<meaning>` | `path:line · symbol` | `<requirement, caller, test, or source>` |

**Evidence gaps:** [list missing requirements, unavailable callers, dynamic dispatch, or framework bindings]

---

## Rule decisions

| Target | Rule | Decision | Evidence | Impact | Necessity | Recommendation or disposition |
| --- | --- | --- | --- | --- | --- | --- |
| `path:line · symbol` | `SRP-C01` | `pass` | `<cited evidence>` | `none` | `none` | `<reasoned disposition>` |

Necessity values: `none` · `optional` · `planned` · `before-change` · `immediate`

---

## Optional technical observations

[Read-only checks used to substantiate findings — command or inspection, result, and any unavailable or unrun checks. No artifacts were modified.]

---

## Completion gates

| Gate | Status | Notes |
| --- | --- | --- |
| Scope | ☐ complete / ☐ incomplete | |
| Semantic evidence | ☐ complete / ☐ incomplete | |
| Rule analysis | ☐ complete / ☐ incomplete | |
| Recommendation | ☐ complete / ☐ incomplete | |
| Read-only contract | ☐ satisfied | No artifacts modified. |
