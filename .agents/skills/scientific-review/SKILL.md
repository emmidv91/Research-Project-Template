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