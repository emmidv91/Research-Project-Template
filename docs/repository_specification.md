# Generic AI-assisted research repository: implementation specification

Prepared 2026-10-09. This document is a complete specification to implement in a Git repository. It is not an installed skill package and does not contain actual research findings.

## 1. Architecture and rationale

Keep exactly two scientific-memory files: a chronological notebook and a current knowledge base. Put all computation under `code/`, evidence under `results/`, and polished writing under `report/`. One root `AGENTS.md` carries standing rules; four instruction-only skills carry task procedures. Do not add databases, agent orchestration services, separate hypothesis files, or a separate task tracker.

The closed loop is:

question → read current knowledge → formulate testable hypothesis/model → investigate → preserve evidence → compare with scientific base → update knowledge and log → choose next question → repeat.

Chat supplies ideas at any stage. Its useful output is distilled into the two memory files before it becomes a dependency. A report update branches from reviewed knowledge; it is not the end of the loop.

Ownership is a workflow convention, not a product access guarantee. Work and Codex must actually receive the same repository revision or explicit handoff files. A chat does not automatically see another surface's filesystem. Repository-local skills are discoverable by Codex; using their procedures in Work requires providing the files or separately installing an appropriate Work skill. This specification does not install Work skills or configure account integrations.

### Evidence behind the design

The following sources were consulted on 2026-10-09. They inform design choices; the exact two-file memory model and approval boundaries are project policies, not claims that these sources prescribe this architecture.

- OpenAI, [Custom instructions with AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md): repository instruction discovery and layered guidance. Use a short root file, without unnecessary nested overrides.
- OpenAI, [Build skills](https://learn.chatgpt.com/docs/build-skills): repository discovery under `.agents/skills`, required name/description metadata, progressive loading, focused instruction-only procedures. Optional `agents/openai.yaml` is omitted here.
- Wilson et al. (2017), [Good enough practices in scientific computing](https://doi.org/10.1371/journal.pcbi.1005510): practical project organization, explicit dependencies, preservation of raw data and processing steps, version control, and avoiding duplication.
- National Academies (2019), [Reproducibility and Replicability in Science, chapter 3](https://www.nationalacademies.org/read/25303/chapter/6): distinguish recomputation with original code/data from independent studies with new data. Reproducing a computation alone does not establish its broader scientific interpretation.
- Schnell (2015), [Ten Simple Rules for a Computational Biologist's Laboratory Notebook](https://doi.org/10.1371/journal.pcbi.1004385): dated notebook entries, intermediate evidence, and links to versioned code/data. Only notebook practices are adopted; this template makes no legal-record claim.
- NIST, [AI RMF Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/): explicit human/AI responsibilities, knowledge limits, evaluation and oversight. The human boundaries below adapt these principles to scientific work.

No external research-agent framework is copied. Skills structure tasks; they do not provide scientific authority.

## 2. Repository tree

```text
research-project/
├── README.md
├── AGENTS.md
├── .gitignore
├── research/
│   ├── research_log.md
│   └── scientific_knowledge.md
├── code/
│   └── .gitkeep
├── results/
│   └── .gitkeep
├── report/
│   ├── main.tex
│   ├── references.bib
│   └── figures/
│       └── .gitkeep
└── .agents/
    └── skills/
        ├── research-investigation/SKILL.md
        ├── computational-investigation/SKILL.md
        ├── scientific-review/SKILL.md
        └── report-update/SKILL.md
```

The three `.gitkeep` files are empty directory placeholders. No supporting README is needed. After the first real computation, add a suitable dependency declaration/lock under `code/` and run folders under `results/`. Do not choose a scientific stack before a task needs one. Optional raw-data storage can be added later, with immutable inputs and documented access; do not treat raw inputs as generated results.

## 3. File: README.md

```markdown
# Research project

A lightweight repository for scientific research assisted by Chat, Work, and Codex. Git stores the durable project state. The researcher remains responsible for scientific conclusions.

## Layout

| Path | Purpose |
| --- | --- |
| `research/research_log.md` | Dated research history, useful reasoning summaries, dead ends and corrections |
| `research/scientific_knowledge.md` | Current objective, theory, facts, assumptions, hypotheses, results, discrepancies and next investigations |
| `code/` | Models, simulations, analysis, plotting, tests and dependency declarations |
| `results/` | Computational evidence, validation outputs and per-run JSON provenance |
| `report/` | LaTeX manuscript, bibliography and reviewed figures |
| `AGENTS.md` | Standing instructions for agents working in this repository |
| `.agents/skills/` | Four focused research procedures |

There are exactly two scientific-memory files. Instructions, code and run metadata support them; they do not become additional stores of scientific conclusions.

## Responsibilities

- Chat is the scientific whiteboard: brainstorm, derive informally, challenge assumptions and explore interpretations. Transfer only useful summaries into repository memory.
- Work coordinates investigations: read knowledge, check sources, formalize hypotheses, review evidence and maintain current understanding.
- Codex implements and validates computations: produce reproducible evidence, document limitations and request scientific review.
- The human researcher sets objectives and approves major conclusions, important changes of method, replacements of accepted interpretations, and major manuscript claims.

These are responsibilities, not exclusive tool capabilities. When necessary Codex can explicitly run the scientific-review procedure, but it must preserve human-review boundaries. Code success is not a scientific review.

## The research loop

1. Read current knowledge and identify the question.
2. State the model, assumptions, prediction and discriminating test.
3. Perform analytical, computational or experimental investigation.
4. Save evidence and provenance.
5. Compare results with theory, limits, previous results, literature and observations where available.
6. Update knowledge: support, qualify, contradict or leave the question inconclusive.
7. Append the research history and identify the next investigation.
8. Repeat. Update the report only for sufficiently mature findings.

An investigation is reviewed only when step 5 has an explicit outcome and steps 6–7 are recorded. Pending human decisions remain visible; they do not prevent routine evidence gathering.

## Start a task

Read `AGENTS.md`, this README and `research/scientific_knowledge.md`. Read the latest log entry and earlier entries referenced by the relevant claims. Identify the question ID or create one in Open Questions. Use `$research-investigation` to formalize a test, then `$computational-investigation` if computation is needed.

Record this compact task contract in Next Investigations, with the reasoning and alternatives in the log:

- Question and linked claim IDs.
- Model/equations, assumptions, domain and units.
- Predictions and evidence that would challenge them.
- Inputs, parameter ranges and desired outputs.
- Numerical/analytical checks, metrics and acceptance criteria.
- Resource limits and review owner.

Do not invent missing physical inputs. State uncertainties or ask for essential missing information. Exploratory tests are allowed; label them and record later changes to the test plan.

## Move between Chat, Work and Codex

Use a shared Git repository when available. Before each handoff, name the branch and commit, linked question/hypothesis IDs, relevant paths, requested work and expected outputs. Record the task in the memory files; a handoff message need not be archived separately.

If Work or Chat cannot access the repository, provide the current two memory files and relevant code/results, or explicitly provide access through an available integration. Bring resulting changes back as a reviewed diff. Do not assume automatic synchronization or that conversations share files.

Allow one writer at a time for the memory files. Parallel computations can use separate branches/run folders. Reconcile memory changes against the latest revision rather than replacing files with older copies.

## Computational evidence and reproducibility

Use unique run folders such as `results/2026-10-09T161200Z_Q-001_trial-01/`. Preserve data needed to check conclusions, machine-readable validation evidence, figures and a `manifest.json`. No per-run Markdown report is required. Link the run in the knowledge base and log.

The manifest records the rerun command, model/code identity, input identities, parameters and units, numerical method and tolerances, software environment, random seeds where applicable, checks actually executed, outputs and limitations. Use `null` with an explanation for unavailable fields, never fabricated versions or successful checks.

A clean code commit is preferred. A dirty run must preserve the relevant patch and any untracked computational inputs, with checksums; a dirty flag alone cannot reconstruct the run. Preserve raw data, document preprocessing and avoid overwriting prior evidence.

After the first implementation, document installation, run and test commands here. Use one appropriate dependency/lock strategy under `code/`; do not add several competing environment systems.

## Review and reporting

Use `$scientific-review` on new evidence. Review assumptions, applicable regimes, analytical limits, literature scope, earlier results, uncertainty and numerical checks. Record discrepancies explicitly. Missing checks produce qualified or inconclusive conclusions.

A numerically checked result is scoped to its model, tested domain and tolerance. It is not proof that the model describes nature. Hypotheses have evidence statuses; results have separate verification labels. See the knowledge file for definitions.

Use `$report-update` after review. Cite literature with inspected sources and verified bibliography metadata. Trace numerical claims and figures to result IDs/run folders. Keep unresolved major claims in knowledge until human approval; do not silently promote them in prose.

Build the starter report from `report/`:

    pdflatex -interaction=nonstopmode -halt-on-error main.tex
    bibtex main
    pdflatex -interaction=nonstopmode -halt-on-error main.tex
    pdflatex -interaction=nonstopmode -halt-on-error main.tex

The initial report has no substantive claims or citations. BibTeX supports later additions; skip it while the bibliography is unused. `latexmk -pdf main.tex` is an alternative if installed.

## Git and data

Follow the version-control policy in `AGENTS.md`. Record the repository collaboration mode here as `solo` or `collaborative`, based on active human contributors. Solo projects allow direct commits to the primary branch without required pull requests; projects with multiple active human contributors use branches and pull requests for substantive changes. AI agents do not affect this classification. When initializing the repository, use the researcher's stated collaboration context; if it is unknown, leave the mode unspecified rather than inferring it from AI agents or historical commit authors.

Use focused commits and inspect diffs. Track the two memory files, instructions, code, configuration, small evidence, manifests, figure sources and manuscript. Do not commit secrets, environments or caches. Commit author information and log contributor fields record activity; they are not authorship judgments.

For large data choose Git LFS or durable external storage according to project needs. Record stable identifiers, checksums, versions and retrieval instructions; manifests stay in Git. External storage must be backed up and accessible to collaborators. No blanket result/data/figure ignore rule is used.

## New collaborator checklist

Read the instructions and current knowledge, inspect Next Investigations and pending decisions, follow evidence links, then consult the log for history. If inputs, sources or provenance are missing, report the gap before relying on the affected claim. No private Chat history should be necessary.
```

## 4. File: AGENTS.md

```markdown
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
```

## 5. File: research/research_log.md

```markdown
# Research log

Chronological scientific notebook. Append substantive sessions below. Use actual timestamps with UTC offset and stable session IDs such as L-001. Summarize scientific reasoning, not hidden AI chain-of-thought. Keep dead ends, alternatives and superseding corrections. A concise session can omit irrelevant fields; never fabricate work to fill the template.

## Entry template (copy below Entries when used)

### L-NNN — YYYY-MM-DDTHH:MM:SS±HH:MM — Descriptive title

- Contributor / role: [human or agent; identify responsible researcher when relevant]
- Repository context: [branch, known commit; describe relevant uncommitted changes]
- Question / linked IDs: [Q-, H-, F-, R-, D-; identifiers actually present]
- Context and objective: [why this investigation matters]
- Reasoning summary and approaches considered: [concise justification, alternatives, rejected routes]
- Hypotheses and predictions: [testable statements; expected and disconfirming outcomes]
- Analytical work: [equations, assumptions, derivation location/summary and checks]
- Computational / experimental work: [what actually happened; commands/run or input links]
- Evidence: [observations and uncertainty, supporting/opposing evidence, inspected sources]
- Scientific comparison: [theory, limits, prior results, literature; scope mismatches]
- Interpretation / review outcome: [support, partial support, contradiction, inconclusive, new regime or numerical/model issue; separate observation from explanation]
- Decisions / human review: [D-ID; Proposed, Pending Human Review or Accepted; approver/date only when known]
- Knowledge changes: [IDs/sections changed, previous → new state, reason; or none]
- Unresolved issues / limitations: [gaps, anomalies, failed/skipped checks]
- Next actions: [specific test/question, owner and criterion]
- Supersedes / corrects: [earlier L-/claim IDs when applicable]

## Entries

No research sessions recorded yet. Remove this sentence when the first real entry is appended. The template above is not a research event.
```

## 6. File: research/scientific_knowledge.md

```markdown
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
```

## 7. File: .agents/skills/research-investigation/SKILL.md

```markdown
---
name: research-investigation
description: Formalize a scientific question using current project knowledge, inspected literature, theory and testable hypotheses. Use for new investigations or formalizing brainstorming; not for computational execution or final result review.
---

# Research investigation

Read root `AGENTS.md` and the two scientific-memory files; follow standing policies without duplicating them.

1. Identify the question, current understanding, applicable facts/theory, unresolved discrepancies and relevant history. If the question is new, allocate a Q-ID. Establish scope and essential missing inputs.
2. Inspect relevant primary literature and authoritative methodological sources. Record actual source locations, definitions and applicability. Separate source statements from your inferences. If access is limited, state that limitation; do not present an uninspected citation as established evidence.
3. State notation, dimensions, governing equations, assumptions, approximations and known limits. Develop inspectable analytical relations when useful, checking algebra, units and limiting behavior. Record the concise derivation in the knowledge framework or result entry and the session summary in the log; do not create a third scientific-memory file.
4. Formalize the hypothesis with scope, measurable prediction, competing explanations and an outcome that would weaken/reject it. Use Proposed or Testing; do not promote intuition into facts.
5. Design the smallest discriminating investigation. Define inputs, range, observables, metrics, checks, uncertainty targets and budget. Identify analytical, numerical or experimental work needed. Separate confirmatory criteria from exploratory sweeps.
6. Update appropriate knowledge sections: question, hypothesis, assumptions/theory, references and Next Investigations. Record disagreements under Contradictions and Anomalies. Append a dated log summary containing alternatives and rationale.
7. For computations, provide a handoff referencing Q-/H-IDs, model/equations, inputs/units, configuration, outputs, checks, criteria and code revision. Identify the review owner and require scientific-review after evidence exists. For major methodological changes, leave a concrete D-ID proposal pending approval while routine investigation continues.

Finish with a testable question, linked knowledge entries, task contract, inspected sources/limitations and next action. Do not report investigations that were only planned as executed.
```

## 8. File: .agents/skills/computational-investigation/SKILL.md

```markdown
---
name: computational-investigation
description: Implement models, simulate, analyze data, validate numerics and generate reproducible evidence for a defined research question. Use for computational execution or reproduction; not for accepting broad scientific conclusions or drafting manuscript claims.
---

# Computational investigation

Read root `AGENTS.md`, the current knowledge, task contract and relevant log/history. Inspect existing code and evidence before replacing an implementation.

1. Confirm the numerical question, model/equations, assumptions, units, inputs, parameter ranges, observables and test criteria. If a necessary model/input is undefined, resolve it or explicitly label a bounded exploratory test. Do not silently choose scientific assumptions.
2. Implement under `code/`. Keep model, configuration and plotting responsibilities clear using functions/files as needed; avoid unnecessary frameworks. Add one appropriate dependency declaration/lock and document exact run/test commands in the root README.
3. Test scientifically meaningful behavior: analytical benchmarks or independent references, known limits, units, sign/normalization conventions and relevant invariants. Check behavior that would expose mistakes rather than reproducing the implementation formula in a test.
4. Assess convergence with appropriate resolution/tolerance/domain/sample changes; measure changes against the observable's agreed criterion. Assess stability and floating-point sensitivity where relevant. For stochastic/statistical analyses record seeds, repetitions, uncertainty, selection/preprocessing and applicable fitting diagnostics. Record skipped/not-applicable checks and reasons.
5. Run within the task budget. Preserve failures or unexpected results when scientifically useful. Store raw evidence and validation metrics in a unique `results/` run folder; generate figures from saved data when practical. Do not overwrite cited evidence.
6. Create `manifest.json` with actual provenance: command/cwd, code commit or reconstructible dirty snapshot, input identities/checksums, resolved parameters/units, method/tolerances, environment, checks, output hashes and limitations. Archive untracked computational inputs when needed. Record completion/failure honestly.
7. Add or update an R-ID in Pending or Unverified Evidence, with run links, observation, checks and limitations. Append a log entry; set the task to Awaiting Scientific Review. Do not place the observation in Verified Results solely because checks pass.
8. Hand evidence to the review owner with expected-versus-observed comparison, checks executed, missing checks, uncertainty, provenance and alternative explanations. If explicitly assigned to complete review, invoke scientific-review as a distinct procedure. Never treat computation itself as hypothesis acceptance.

Finish with actual commands/check outcomes, evidence locations, scoped observations, limitations and review next action. A successful run is computational evidence, not an automatic scientific conclusion.
```

## 9. File: .agents/skills/scientific-review/SKILL.md

```markdown
---
name: scientific-review
description: Review new analytical, numerical or experimental evidence against current theory, literature, assumptions and prior results, then update scientific memory and next questions. Use after investigations or when results conflict; not as a substitute for producing missing evidence.
---

# Scientific review

Read root `AGENTS.md`, current knowledge, relevant log history, new evidence/manifests and the original test contract. This procedure closes the scientific feedback loop.

1. Check that evidence belongs to the stated model and revision. Inspect input identity, units, parameter domain, executed checks, convergence/stability, uncertainty and completeness. Separate reproduced computation, verified implementation and validation against observations. Missing provenance or failing critical checks limits the inference.
2. Reconstruct expectations from governing equations, assumptions, approximations, known limits, literature, earlier verified results and experiments where available. Inspect relevant sources when comparison requires them. Check definitions/regimes before declaring a contradiction. Record unavailable comparison categories explicitly.
3. Compare observations quantitatively where possible. Assess whether the test discriminates the hypothesis from alternatives; agreement alone is insufficient. Distinguish numerical error, statistical variation, model inadequacy, source-scope mismatch and potentially new behavior. Do not call a regime novel without checking relevant prior work.
4. Record one or more scoped outcomes: supports; partially supports; contradicts; inconclusive; exposes numerical/modeling issue; reveals candidate new regime; requires new hypothesis. Explain evidence and limits. If applicable, assign a method-specific result verification label only after checks meet criteria. Failed or missing critical checks mean Not Yet Verified or Inconclusive.
5. Update knowledge deliberately:
   - Hypotheses: support status, opposing evidence and remaining alternatives.
   - Results: reviewed R-ID and verification scope; move out of pending evidence only if justified.
   - Anomalies: preserve X-ID with conflicting claims, scope checks and next discriminating test.
   - Open Questions: answer, qualify or open follow-up Q-IDs.
   - Decisions: concrete proposals/approval references for major changes.
   - Current Understanding: concise evidence-linked synthesis, including pending decisions.
   - Next Investigations: next test, owner, criteria and task status.
6. Never silently change the knowledge base to agree with a new output. Preserve superseded claims with links and append a correction/superseding log entry. Flag defective prior evidence immediately. Do not fabricate human approval; major interpretation changes remain pending while factual evidence and discrepancies are recorded.
7. Append the dated review entry with comparisons, outcome, exact knowledge/status changes, limitations and next action. Link the computation/analysis session and run evidence. Do not create another scientific-memory document.

Finish with review disposition, what changed in knowledge, what remains uncertain, human decisions needed and the next investigation. The loop has a recorded feedback outcome even if the outcome is inconclusive or awaiting human acceptance. Do not label a compute-only handoff reviewed.
```

## 10. File: .agents/skills/report-update/SKILL.md

```markdown
---
name: report-update
description: Transfer reviewed, sufficiently mature findings into the LaTeX report with verified citations and traceable figures. Use for manuscript updates after scientific review; not for establishing hypotheses or resolving unreviewed evidence.
---

# Report update

Read root `AGENTS.md`, relevant reviewed knowledge, human decisions, report and supporting evidence. Use current knowledge as the scientific basis, not a Chat conversation.

1. Identify eligible F-/R-/H-/D-IDs and their limits. Ensure substantive scientific review exists. Check that major new manuscript claims have human acceptance for their scope. Prepare proposals in knowledge if approval is missing; continue eligible routine edits.
2. Inspect source support for literature claims and verify bibliographic metadata before adding citations to `report/references.bib`. Use stable citation keys shared with the knowledge references. Do not invent bibliography entries or imply a broader source claim.
3. Inspect numerical/experimental/analytical provenance for each reported result. Trace values, uncertainty and domain to an R-ID and supporting evidence. Distinguish result statements from interpretations. Include unresolved issues only as explicitly framed limitations or questions, without promoting them into conclusions.
4. Edit `report/main.tex`; add sections files only when the manuscript is genuinely too large to maintain as one file. Use precise language, defined notation, stated approximations and measured uncertainty. Do not strengthen “supported” into “proved”.
5. Use figures generated from reviewed evidence. If copying into `report/figures/`, retain the source result as authoritative and add a nearby TeX comment recording R-ID, source path, generating command/script and source hash. Verify the copied figure matches the referenced source. Record any postprocessing, including crop/style changes.
6. Add nearby TeX comments for computational claims identifying R-ID/run/manifest; keep literature citations visible in prose. Comments support traceability, not reader-facing claims.
7. Compile changed LaTeX where tools exist. Resolve citation/reference errors and inspect the rendered output when layout changes. Report missing tools, unresolved warnings or failed compilation accurately.
8. Append a log summary identifying report sections, claim IDs, evidence, actual build checks and next action. Update knowledge only if reporting exposes a scientific issue; route that issue back through scientific-review rather than editing knowledge to fit the prose.

Finish with changes, claim/evidence links, actual report checks and any excluded pending claims. Report writing remains downstream of scientific review.
```

## 11. File: .gitignore

```gitignore
# Python environments and bytecode
__pycache__/
*.py[cod]
.venv/
venv/
env/
ENV/
.python-version.local
*.egg-info/
.eggs/

# Test, type and formatting caches
.pytest_cache/
.mypy_cache/
.ruff_cache/
.tox/
.nox/
.coverage
.coverage.*
htmlcov/

# Notebook checkpoints (keep notebooks)
.ipynb_checkpoints/

# Local secrets/config (keep example configuration)
.env
.env.*
!.env.example

# Editor-local metadata
.vscode/
.idea/
*.swp
*.swo
*~

# OS temporary files
.DS_Store
Thumbs.db
Desktop.ini

# LaTeX build products, scoped to report
report/**/*.aux
report/**/*.bbl
report/**/*.blg
report/**/*.fdb_latexmk
report/**/*.fls
report/**/*.log
report/**/*.out
report/**/*.synctex.gz
report/**/*.toc
report/**/*.lof
report/**/*.lot
report/**/*.nav
report/**/*.snm
report/**/*.vrb
report/main.pdf

# Intentionally keep small data, provenance, validation logs and figures.
# Do not add blanket rules for results/, *.csv, *.json, *.h5, *.png or *.pdf.
# Add specific rules for external large data only after documenting retention.
```

`report/main.pdf` is an easily rebuilt preview; release PDFs can be explicitly tracked elsewhere. LaTeX log ignores are report-scoped so numerical validation logs remain trackable. Compiled-language outputs can receive narrow ignore rules if that language is introduced; this starter does not presume it.

## 12. File: report/main.tex

```latex
\documentclass[11pt]{article}
\usepackage[margin=1in]{geometry}
\usepackage{amsmath,amssymb}
\usepackage{graphicx}
\usepackage{booktabs}
\usepackage[hidelinks]{hyperref}
\graphicspath{{figures/}}

\title{Research Project: Working Report}
\author{Research team}
\date{\today}

\begin{document}
\maketitle

\begin{abstract}
This document is a report scaffold. No scientific findings have yet been
entered. Reviewed findings will be added with their scope, uncertainty,
citations and computational provenance.
\end{abstract}

\section{Research objective}
Define the question, motivation and scope after project initialization.

\section{System and theoretical framework}
Define observables, notation, assumptions, governing equations,
approximations and their domains of applicability.

\section{Methods and validation}
Describe analytical, computational or experimental methods, inputs,
convergence checks, controls and uncertainty estimates.

\section{Results}
Insert reviewed findings only. Each computational claim should have a
nearby source comment identifying its result ID and evidence manifest.
% Example format only: R-ID; results/<run-id>/manifest.json; observable/data locator.

\section{Discussion and limitations}
Separate observations from interpretations. Discuss alternatives,
applicable regimes and unresolved discrepancies explicitly.

\section{Conclusions and next questions}
Summarize approved conclusions with their limits and identify open questions.

% Add verified citation entries and \cite{key} commands when sources are used.
% No placeholder scientific citation is inserted in this scaffold.
\bibliographystyle{plain}
\bibliography{references}

\end{document}
```

## 13. File: report/references.bib

```bibtex
% Project bibliography. Intentionally empty until project sources are inspected.
% Add verified bibliographic records with stable keys matching the References
% section of research/scientific_knowledge.md.
% Workflow-design sources belong to the implementation specification;
% they are not automatically project-science citations.
```

## 14. Lightweight provenance contract

This is a convention, not an additional permanent template file or a requirement for a generic manifest validator. Create a populated `manifest.json` only when a real meaningful run exists. Keep resolved configuration in the manifest for small tasks; point to a hashed configuration file if it grows. Do not maintain two independently edited copies of parameters.

Example shape (illustrative placeholders, not an actual run):

```json
{
  "schema_version": 1,
  "run_id": "<unique timestamp and task suffix>",
  "created_at": "<ISO-8601 timestamp with offset>",
  "question_ids": ["Q-001"],
  "hypothesis_ids": ["H-001"],
  "result_ids": ["R-001"],
  "execution_status": "completed",
  "command": "<exact command>",
  "working_directory": "<repository-relative cwd>",
  "code": {
    "commit": "<full source commit SHA or null>",
    "dirty": false,
    "snapshot": null,
    "files": [{"path": "code/<script>", "sha256": "<hash>"}]
  },
  "model": {"definition": "<knowledge section/model label>", "assumptions": ["<links>"]},
  "inputs": [{"locator": "<path or durable identifier>", "version": "<version>", "sha256": "<hash>", "access": "<retrieval instructions>"}],
  "parameters": {"B": {"value": 1.0, "unit": "<defined unit or dimensionless>"}},
  "numerics": {"method": "<method>", "precision": "<precision>", "tolerances": {}, "resolution": {}},
  "environment": {"runtime": "<name/version>", "dependencies": {}, "lockfile": "<path/hash or null>", "hardware": "<only if relevant>"},
  "randomness": {"seed": null, "reason": "<not stochastic, or explain unavailable seed>"},
  "checks": [{"name": "<benchmark/convergence/etc>", "status": "passed", "metric": "<measured error>", "criterion": "<predefined threshold>", "evidence": "<validation output path>"}],
  "outputs": [{"path": "<run-relative file>", "sha256": "<hash>", "description": "<observable and units/column definitions>"}],
  "limitations": ["<actual limitations>"],
  "scientific_review": "pending; current disposition is maintained under R-001 in scientific_knowledge.md"
}
```

Use `[]` for absent inputs and checks genuinely not required; do not populate fictitious IDs. Record failed/skipped checks, not just passes. A dirty snapshot must preserve changed tracked files through a patch plus untracked sources/configurations needed for reconstruction. If no source commit exists, archive the actual executed code/configuration. Hash the input files and generating code, not just final figures. Preserve input units, preprocessing, fit selection and random-number configuration where applicable.

The manifest is immutable execution provenance. Current scientific disposition lives in the knowledge file, avoiding conflicting mutable review states. Later reruns use new run IDs and link earlier runs. Not every intermediate scratch output needs retention; evidence underlying claims, anomalies and meaningful failures does.

## 15. Who executes each stage

| Stage | Primary owner | Persistent output | Human boundary |
| --- | --- | --- | --- |
| Brainstorm and challenge explanations | Chat + researcher | Useful ideas distilled into H/Q entries and log | Choose promising directions |
| Inspect literature and formalize question | Work | Facts/references, theory, hypothesis, task contract | Major objective/method changes |
| Derive analytical predictions | Work or assigned agent | Framework or scoped analytical R entry | Accept major interpretation |
| Implement/run/check computations | Codex | Code, evidence, manifests; pending R and log | Routine implementation autonomous |
| Compare evidence with scientific base | Work; Codex if explicitly assigned review | Reviewed R/H/X/Q/D changes and synthesis | Resolve major scientific acceptance |
| Collect/assess experiments | Researcher; tools assist analysis | Input evidence and scoped experimental R | Actual experimental conduct and scientific responsibility |
| Choose next investigation | Work + researcher | Next Investigations/Q updates | Major direction changes |
| Update manuscript | Work or Codex using report-update | LaTeX, bibliography, traced figures, log | Major new manuscript claims |
| Commit and synchronize | Current authorized repo writer | Git revision and handoff | Merge/push/publication within authorization |

A single person can perform all human roles. Do not introduce a review committee or require approval of routine file edits. Evidence gathering and concrete review proposals proceed before asking for a scientific decision.

## 16. Final design audit and loop demonstration

| Audit item | Design outcome |
| --- | --- |
| Duplication | Claim details stored once; summaries link IDs. Manifest stores execution provenance, memory stores interpretation. BibTeX is manuscript citation metadata, not another scientific-memory file. |
| Complexity | One computation area, four instruction-only skills, no mandatory orchestration/CI/schema tooling. |
| Memory fragmentation | Exactly two scientific-memory Markdown files; no per-run Markdown reports. |
| Ownership | Codex delivers evidence; scientific-review delivers feedback. Cross-surface access and synchronization are explicit. |
| Overpromotion | Hypothesis support, result verification and human acceptance are separate fields. |
| Feedback | Every reviewed investigation updates relevant knowledge, log and next actions, including inconclusive outcomes. |
| Contradictions | X entry plus correction/superseding log and pending decision; incompatible evidence survives. |
| Provenance | Commands, input/code identity, units, environment, checks and hashes; dirty runs are reconstructible. |
| Reporting | Reviewed evidence, scoped language, source citations and computational trace comments. |
| Daily maintenance | One compact log entry and targeted knowledge edits per meaningful session; omit irrelevant template fields. |
| Fresh-agent continuity | Objective, state, pending decisions, evidence and next test in repository; no required Chat history. |

Illustrative loop (not seeded into project files):

1. Chat suggests H-001: observable A might change monotonically with parameter B in model M.
2. Work reads existing facts/theory, formalizes Q-001/H-001, states domain and a discriminating test in Next Investigations.
3. Codex implements model M, tests limits and convergence, and saves a parameter sweep with a manifest. R-001 is pending scientific review.
4. Review finds behavior differs in part of the domain. It checks units, definitions, numerical convergence and assumptions rather than changing the expected behavior to fit the plot.
5. If evidence is sound, review records partial support or contradiction, creates X-001 as appropriate, records scoped numerical verification of R-001 and updates Current Understanding. A changed major explanation is a pending D-001 proposal.
6. Review appends a log entry and opens Q-002: which assumption or regime explains the discrepancy? A concrete next test is queued. Human approval, if needed, is recorded later in D-001 and the log.
7. Report-update includes only eligible reviewed findings and approved major claims. It does not terminate inquiry; Q-002 initiates the next loop.

This closes the loop even when the best scientific conclusion is “inconclusive”. It does not pretend that a pending human decision is accepted.

## 17. Codex implementation instructions

Attach this complete document to Codex and paste the prompt below. Launch Codex in the intended repository or an empty destination. Do not ask Codex to infer these files from conversation history.

```text
Implement the attached Research_Repository_Codex_Specification.md as a complete generic research repository.

First inspect the current directory, Git status and applicable instructions. If this is an existing repository, preserve unrelated work and adapt paths without overwriting existing research. If empty, create the scaffold here; do not create a redundant nested repository. Initialize Git only if no repository exists.

Create the exact complete file contents from sections 3–13 at their stated relative paths. Create the three empty .gitkeep files. Do not copy the specification itself into scientific memory. Do not create scientific claims, actual run manifests, sample hypotheses, fake sessions or fake bibliography entries. Do not install these skills globally or configure Work integrations. Keep exactly the two specified scientific-memory files and the consolidated code/ area. The four SKILL.md files are repository-local instruction-only skills.

Use the existing skill-creator/validator if available and applicable, while preserving the specified repo-local location and avoiding unnecessary extras. Otherwise validate required YAML name/description, matching directory names and readable Markdown directly. Optional agents/openai.yaml is not required.

Check:
- expected file paths and exact memory-file count;
- four skill frontmatters and focused procedures;
- closed feedback paths and separate verification/acceptance rules;
- no blanket ignores for evidence, manifests or figures;
- valid relative references and no project-specific scientific content;
- report/main.tex compiles with pdflatex if available (initial bibliography is empty, so skip BibTeX until citations exist).

If compilation is available, inspect the PDF and report the actual outcome. If unavailable, say so without claiming compilation. Do not add a simulation just to test an empty generic project.

Follow the repository collaboration mode and the Version control section of AGENTS.md. Record the mode in README.md when the active human contributor context is known. For solo projects, direct commits to the primary branch are acceptable and pull requests are not required. For multiple active human contributors, make substantive scaffold changes on a branch for integration through a pull request. AI agents do not count as human collaborators.

Inspect the final diff. Make a focused initial scaffold commit if repository policy and configured Git identity permit it; stage only scaffold changes. Never fabricate a Git identity. Leave changes ready to commit if identity/policy prevents committing. Do not push, merge, publish or change remotes without existing authorization.

Finish with the created tree, checks actually performed, any limitations, and the next concrete step: initialize Research Objective and System / Problem Definition from the researcher's project description using research-investigation. Do not ask routine permissions or stop after proposing a plan.
```

After implementation, give Work the same committed memory and relevant files. The first scientific task is project initialization, not a generic example simulation. Define an actual objective, system, notation, existing evidence and first question before selecting dependencies or computational methods.

## 18. Specification checks performed

Extracted all 11 file-content blocks into a temporary verification directory. Confirmed the four skills have valid YAML name/description fields matching their directory names and that research contains exactly two memory files. Compiled the supplied LaTeX scaffold with pdfLaTeX successfully to a one-page PDF; the intentionally unused bibliography produces no bibliography content. These checks validate the scaffold, not a future project's science or runtime integrations.
