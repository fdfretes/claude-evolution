# Iteration 62: Misapplication Recovery Lens

## Lens Description
When a practitioner makes an honest mistake in applying a rule (not adversarial gaming, not missing sections — just misunderstanding), does the system of rules create feedback loops that surface the error before it reaches production?

## Distinction from Previous Lenses
- **Adversarial compliance (iter 60)**: Intentional gaming of rules → tests letter-vs-spirit pairing
- **Partial adoption (iter 61)**: Missing entire sections → tests section independence
- **Misapplication recovery (iter 62)**: Honest misunderstanding of specific rules → tests feedback loop adequacy

## 8 Scenarios Tested

### CAUGHT (3 scenarios — existing mechanisms reliable)

**Scenario 1: HTTP client in core/** — Developer thinks "external" means outside repo.
- Test friction (can't write pure tests for impure core) + architecture review checklist → reliably caught by 2 independent mechanisms.

**Scenario 4: Zod in core/** — Developer adds validation deep in stack.
- If using Zod: caught by "core/ zero external imports" rule (different rule than intended but effective).
- If hand-rolled: SILENT (see below), but code quality issue only, not correctness.

**Scenario 6: One giant commit per PR** — Developer avoids splitting to maintain atomicity.
- Law 2 (separation of concerns) + Newspaper Test + "and" test within Law 1 → caught by 3 independent mechanisms.

### PARTIALLY CAUGHT (3 scenarios — detection depends on reviewer diligence)

**Scenario 2: 15-field options object** — Developer treats rule as permission for unbounded parameter surfaces.
- Review might catch via "unnecessary complexity" + 30-line function limit creates indirect pressure.
- No mechanical gate. But this is a code quality issue, not correctness.

**Scenario 3: Non-failing regression test** — Test passes both before and after fix.
- Phase 4 commit structure (Commit 1 must fail) is designed for this. But depends on per-commit CI or reviewer manually verifying Commit 1 fails.
- Adding CI-specific enforcement would violate document's tool-agnostic approach.

**Scenario 7: Never mock anything** — Developer interprets "mock at boundaries only" as discouraging mocks.
- Flaky test rule (lagging indicator) + CI pipeline stage separation + review.
- Document text is clear ("mock adapters like DB and HTTP") — misapplication requires selective reading.

### SILENT (2 scenarios — no reliable feedback mechanism)

**Scenario 5: Enumerate all 30 columns** — Developer lists every column, violating spirit of "select only needed."
- Rule already says both "Never SELECT *" AND "select only the columns you need" in same sentence.
- No mechanical enforcement possible for "only select what you need" without context analysis.
- Code quality/performance issue, rarely causes bugs.

**Scenario 8: Feature flags on everything** — Developer wraps all changes including internal refactoring.
- **RE-EVALUATED**: Section 10 already has FEATURE FLAG LIFECYCLE with type classification (release, ops, experiment, permission). A refactoring is none of these types — reviewer can cite type taxonomy. **Reclassified from SILENT to PARTIALLY CAUGHT.**
- Flag type taxonomy provides structural constraint; reviewer can say "what flag type is this?"

## Structural Observation

**Pattern**: Misapplications creating **structural friction** (can't write prescribed tests, violates binary rule) are reliably caught. Misapplications that are **functionally correct but architecturally suboptimal** (too many fields, too many columns) are caught only by human judgment. This is inherent to any standards document — you can't mechanically enforce "did you select only the columns you need?" without understanding the caller's context.

## Edit Assessment

All findings are below editing threshold:
- Scenario 3 (CI regression test verification): Tool-specific, violates document's tool-agnostic approach
- Scenario 5 (column selection emphasis): Text already says "select only the columns you need" — adding emphasis is redundant
- Scenario 4b (no re-validation in core): Section 6 already says "typed and trusted throughout the service layer" — connection is derivable
- Scenario 8 reclassification: Already handled by existing flag lifecycle rules

**Verdict: Zero edits. 8th consecutive zero-edit iteration.**

## New Low-Severity Observations
- Hand-rolled redundant validation in core/ is not explicitly prohibited (derivable from "typed and trusted" + purity principle)
- Non-failing regression test requires per-commit CI verification or reviewer discipline (existing Phase 4 structure is the correct defense; CI-specifics are tool-dependent)
