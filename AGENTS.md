# Repository instructions

## Context and scope

Read `README.md`, `research/scientific_knowledge.md`, the latest research-log entry and relevant linked history before scientific work. Inspect relevant code, results and report files. Check Git status before editing. Treat unknown project information as unknown.

Keep scientific memory in exactly `research/research_log.md` and `research/scientific_knowledge.md`. Put all computation, including meaningful tests, in `code/`; evidence in `results/`; polished writing in `report/`. Do not create separate top-level src, simulations or tests directories. Keep procedures in the four repository-local skills. Do not add infrastructure without a demonstrated need.

## Scientific rigor

Distinguish literature-supported facts, assumptions, hypotheses, analytical/numerical/experimental results, interpretations and discrepancies. Every substantive claim needs scope and an evidence/source link. Literature claims require inspecting the source and checking applicability; never invent citations, data, derivations or executed checks.

Use hypothesis statuses and result verification labels defined in the knowledge file. “Verified Numerically” applies only to a stated computation/model/domain/tolerance. Code running or matching an expected curve does not establish a hypothesis, prove uniqueness of an explanation or validate a model against nature.

State notation, units, assumptions, approximations, uncertainty and regimes. Define checks and metrics before confirmatory investigation. Preserve exploratory/post-hoc changes to the plan. Prefer tests capable of falsifying an explanation, limiting cases and independent benchmarks over tests that merely repeat implementation.

## Scientific memory

Append meaningful sessions to the log with actual date/time/offset, contributor, question, concise reasoning summary, evidence, decisions, knowledge changes and next actions. Never store hidden chain-of-thought. Omit empty optional fields for short sessions. Correct historical scientific claims with a later entry referencing the original; do not silently rewrite them. Obvious formatting/typographical repairs may be made without changing scientific meaning.

Update the knowledge file as current state. Keep stable IDs, scope, supporting and opposing evidence, status and review provenance. Do not reuse retired IDs. Put each detailed claim in one authoritative section and cross-reference it elsewhere. Log every substantive knowledge change. Retain superseded claims briefly with links to their replacements; record new discrepancies in Contradictions and Anomalies.

Keep unreviewed findings in a clearly labeled pending-evidence subsection. Do not insert them as verified results. When edits conflict, inspect the current revision, reconcile scientifically and preserve both incompatible claims as a discrepancy until resolved. Never merge status changes solely to match a new output.

## Computation and provenance

Read the task contract and model before implementation. Work autonomously on routine implementation and checks within the agreed model. Preserve immutable inputs and document preprocessing. Use explicit configurations and meaningful tests; assess convergence, stability, limits, units and uncertainty as applicable. Record skipped checks and reasons.

Preserve each meaningful run in a unique results folder with `manifest.json`, outputs and actual validation evidence. Record command/cwd, code version, input checksums/locators, parameters/units, method/tolerances, relevant dependencies, seeds, checks, limitations and output hashes. Do not overwrite cited runs. Prefer clean source commits; dirty runs need archived relevant patches and untracked sources/configuration. If provenance is incomplete, say so and restrict claims.

Maintain one appropriate dependency specification/lock under `code/` when dependencies are introduced. Record runtime versions and relevant hardware/precision settings when they affect results. Never claim a command was executed when it was only proposed.

## Scientific review and human boundaries

After evidence generation, use the scientific-review procedure explicitly, or leave the run pending review with its next action. Compare with theoretical predictions, assumptions/regimes, limiting cases, previous results, literature and observations when available. Record outcome, discrepancies, uncertainty and knowledge updates; then formulate the next investigation. A compute-only handoff is allowed but is not a closed loop.

Agents may record scoped evidence and routine review outcomes. Human approval is required before promoting major hypotheses into accepted conclusions, replacing an accepted interpretation, deciding a literature/result contradiction is resolved, adopting an important methodological change as the default, or adding a major new manuscript claim. Draft proposals and gather safe, reversible evidence first. Record approval as a dated D-ID with approver and approved scope. Never invent approval or treat silence as approval. Existing explicit authorization for that scope need not be requested again.

Distinguish evidence status from acceptance: update support/contradiction evidence immediately, while the major interpretive decision remains Pending Human Review. If a previously accepted result has a demonstrated defect, flag it immediately as unreliable/pending re-review and preserve its history; do not keep citing it as sound while awaiting approval. Implement exploratory alternative methods without replacing the accepted default.

## Version control

Use the repository's collaboration mode.

For a solo research project, direct commits to the primary branch are
acceptable and pull requests are not required.

For a project with multiple active human contributors, make substantive
changes on branches and integrate them through pull requests.

AI agents do not count as additional human collaborators when determining
whether the project is solo or collaborative.

## Report and Git

Use report-update only for reviewed, sufficiently mature findings. Source literature claims, trace computational claims/figures to evidence, qualify interpretations and exclude unapproved major conclusions. Build changed LaTeX when a compiler is available and report missing tools or failed checks. Do not create fake project references.

Preserve unrelated user work. Use focused changes/commits; stage only intended files. Do not reset, force-push, change remotes or overwrite evidence to resolve conflicts. Push/merge/publish only within user authorization. For shared memory use one writer or branches with explicit reconciliation. Finish with findings, actual checks, changed paths, limitations, review status and next action.