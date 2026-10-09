# Scientific knowledge

Current scientific state. This file is organized by meaning, not date. The project has not yet been scientifically initialized. Placeholders and templates are not claims.

## Recording rules

Use stable IDs where helpful: F- facts; H- hypotheses; R- results; Q- questions; D- decisions. Add A- assumptions and X- anomalies only when cross-linking benefits the project. Do not reuse IDs. Maintain each detailed claim in one section; other sections link to it. Summaries do not duplicate evidence tables.

Record statement, claim type, scope/regime, evidence/source links, limitations, status and review provenance. Missing evidence is explicit. An inspected source supports only what it actually establishes within its stated assumptions; disagreements between sources remain visible.

Hypothesis evidence statuses:

| Status | Meaning |
| --- | --- |
| Proposed | Testable idea without sufficient assessed evidence |
| Testing | An investigation is in progress |
| Supported | Assessed evidence supports the stated prediction within scope; alternatives may remain |
| Partially Supported | Only part of the statement/domain is supported; state the boundary |
| Rejected | Evidence defeats the stated prediction within its defined scope; retain the reason |
| Inconclusive | Evidence cannot discriminate, is insufficient or has unresolved validity problems |

Result verification labels are separate, and can be combined:

| Label | Required basis |
| --- | --- |
| Unreviewed | Evidence exists but has not undergone scientific comparison |
| Not Yet Verified | Review performed, but required checks are missing or fail |
| Verified Analytically | Inspectable derivation, assumptions/domain and checked algebra/limits; exact result or explicitly stated approximation |
| Verified Numerically | Recorded applicable benchmarks, convergence/stability and error criteria pass for the tested model/domain; reproducible evidence exists |
| Verified Experimentally | Documented measured evidence with calibration/controls/uncertainty and applicable repeatability checks; scoped finding only |

Use “Verified” with a method and scope, never as a universal truth flag. Verification of an implementation differs from validation of a model against observations. An experimental observation can be recorded before experimental verification. A literature fact is Literature-supported, not automatically independently verified by this project.

Human acceptance is a separate decision field: Proposed, Pending Human Review, Accepted, Declined or Superseded. Acceptance does not erase uncertainty. Link major interpretation changes to D-IDs. Routine evidence assessment does not require approval; major scientific acceptance does.

## 1. Research Objective

- Main question: [not yet defined]
- Intended contribution and success criteria: [not yet defined]
- Scope and exclusions: [not yet defined]
- Responsible researcher: [not yet identified]

## 2. System / Problem Definition

[Define the system, variables, observables, inputs, outputs, boundary/initial conditions and available data. Distinguish measured inputs from inferred or assumed quantities.]

## 3. Notation and Conventions

| Symbol / name | Definition | Units / dimensions | Convention / domain |
| --- | --- | --- | --- |

[State normalizations, signs, coordinate conventions, statistical conventions and precision requirements as needed.]

## 4. Established Facts

No facts recorded.

Entry pattern: `F-NNN — statement; Type: literature-supported fact; Scope: ...; Source: reference key + inspected page/section/equation; Limitations: ...; Review: reviewer/date/log link.`

Project-established conclusions must link to the underlying R-/H-IDs and an accepted D-ID for major claims. Do not duplicate the detailed results here.

## 5. Theoretical Framework

### Governing equations

[Equations, definitions, derivation/source links and domain of applicability.]

### Assumptions

[Explicit assumptions and justification; distinguish assumptions from facts. Use A-IDs only when needed.]

### Approximations and regimes

[Error/order estimates where available, applicability and breakdown conditions.]

### Known limiting cases

[Checkable predictions and benchmark expressions, with references/derivations.]

## 6. Hypotheses

No hypotheses recorded.

Entry pattern:

- H-NNN — [statement and scope]
- Status: Proposed / Testing / Supported / Partially Supported / Rejected / Inconclusive
- Basis and assumptions: [F-/A-/theory links]
- Predictions and discriminating test: [metric and criterion]
- Supporting evidence: [R-/run/source links]
- Opposing evidence / alternatives: [links and explanation]
- Limitations: [what has not been established]
- Review: [reviewer/date/L-ID]
- Major acceptance decision: [D-ID or not applicable]

## 7. Verified Results

No verified results recorded.

Entry pattern:

- R-NNN — [precise scoped finding]
- Type: Analytical / Numerical / Experimental
- Verification: [method label(s)]
- Model / assumptions / domain: [links]
- Evidence: [run manifest, data or derivation; source locations]
- Validation checks and uncertainty: [measured error, tolerance, checks and limitations]
- Scientific comparison: [expected versus observed; links to relevant claims]
- Review: [reviewer/date/L-ID; human D-ID if needed]
- Reliability: Current / Pending Re-review / Superseded [reason and replacement link]

### Pending or unverified evidence

No pending evidence recorded. Keep Unreviewed/Not Yet Verified results here with the same R-ID pattern and explicit missing checks. Move a result to Verified Results only after review supports its scoped verification label. Retain unreliable/superseded results briefly with links; never reuse their IDs.

## 8. Contradictions and Anomalies

No discrepancies recorded.

Entry pattern: `X-NNN — conflicting claims/observations; expected versus observed; comparable scope/units checked; evidence links; candidate explanations; status Open / Investigating / Pending Human Review / Resolved; discriminating next test; resolution D-/L-link if resolved.`

Preserve resolved discrepancies and the reason for resolution. Do not erase a contradiction by changing theory to fit an output.

## 9. Open Questions

No questions recorded.

Entry pattern: `Q-NNN — question; why it matters; related IDs; status Open / In Progress / Answered / Deferred; answer or next test links.`

## 10. Scientific Decisions

No decisions recorded.

Entry pattern: `D-NNN — proposal/decision; reason and evidence; scope; consequences; status Proposed / Pending Human Review / Accepted / Declined / Superseded; proposer; approver/date and approval record if accepted; L-ID; supersedes if applicable.`

An agent may propose major decisions, but may not fabricate acceptance. Flag demonstrated defects immediately even if their replacement interpretation awaits human review.

## 11. Current Understanding

[Concise synthesis referencing authoritative F-/H-/R-/D-IDs. Distinguish observations, interpretations and uncertainties. Mention material pending reviews. Do not maintain a duplicate claim inventory.]

## 12. Next Investigations

No investigation queued.

Task contract pattern:

- Question / hypothesis IDs and objective:
- Owner / review owner:
- Model, assumptions, domain and units:
- Prediction and discriminating alternative:
- Inputs / parameters / outputs:
- Method and checks:
- Metric / acceptance criteria and uncertainty target:
- Resource budget / stop conditions:
- Evidence/run links and status: Planned / Running / Awaiting Scientific Review / Awaiting Human Decision / Complete
- Next action:

## 13. References

No project references recorded. Use stable citation keys matching `report/references.bib` when a source enters the manuscript. Record full citation/DOI or stable URL, inspected version/date if relevant, source locator (page/section/equation), supported claim IDs and applicability notes. Mark abstract-only or inaccessible sources as such; do not imply full inspection.