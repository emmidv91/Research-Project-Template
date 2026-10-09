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