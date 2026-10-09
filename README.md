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