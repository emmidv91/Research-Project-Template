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