# Failure Mode Asymmetry Audit - Iteration 49

## Lens Description
Check whether the document's protective density (rules per failure mode) is proportional to failure severity. HIGH-severity failure modes should have the most rules; LOW-severity should have the fewest. If a catastrophic failure mode has fewer rules than an annoying one, that's an asymmetry worth fixing.

## Methodology
1. Enumerate all failure modes the document addresses (explicit or implicit)
2. Classify by severity: CATASTROPHIC (data loss, security breach, production outage), HIGH (broken builds, wrong behavior shipped), MEDIUM (tech debt, maintenance burden), LOW (style, conventions)
3. Count protective rules per failure mode
4. Identify any CATASTROPHIC/HIGH modes with less coverage than MEDIUM/LOW modes

## Failure Mode Inventory

### CATASTROPHIC (production outage, data loss, security breach)
1. **Secret leakage**: S1 Law 4, Pre-Commit Step 3, S6 Secrets Management, S9 Before Submitting, S11 Never Do, S22 rotation — 6+ protective layers ✓ WELL COVERED
2. **SQL injection**: S6 parameterized queries, S21 injection pattern scanning — 2 layers ✓ ADEQUATE (inherently simple: parameterize always)
3. **Data loss from force push**: S1 Law 5, S11 Never Do — 2 layers ✓ ADEQUATE (inherently simple: never do it)
4. **Production manual fix**: S12 anti-pattern, Emergency Hotfix Protocol — 2 layers ✓ ADEQUATE
5. **Missing input validation**: S6 every boundary, S3 Type Safety, S21 CI gate — 3 layers ✓ WELL COVERED
6. **Swallowed errors hiding failures**: S3 Error Handling "criminal/negligent", S11 Never Do, S12 Fix Quality Rule 4 — 3 layers ✓ WELL COVERED
7. **Unintended data exposure in API responses**: S6 Response Serialization Safety (allowlist) — 1 layer, BUT this single rule is comprehensive (the pattern itself is complete) ✓ ADEQUATE

### HIGH (broken builds, wrong behavior shipped)
8. **Breaking commit in shared history**: S1 Law 1 (bisect-safe), S1 Law 4 (Pre-Commit Protocol 6 steps), S12 Phase 4 squash note — 3 layers ✓ WELL COVERED
9. **Untested bug fix**: S12 Phase 1 (reproduce first), Phase 4 (3-commit structure), Anti-patterns (closing without regression test) — 3 layers ✓ WELL COVERED
10. **Speculative fix**: S12 Prime Directive, Phase 1 "NEVER apply speculative fix", Anti-patterns — 3 layers ✓ WELL COVERED
11. **Wrong error bubbling (null check everywhere vs boundary validation)**: S12 Fix Quality Rule 2, Rule 3 — 2 layers ✓ ADEQUATE

### MEDIUM (tech debt, maintenance burden)
12. **Mixed-concern commits**: S1 Law 2 — 1 layer, but comprehensive (lists 5 prohibited combinations) ✓ ADEQUATE
13. **N+1 queries**: S7 — 1 layer, but with concrete fix patterns ✓ ADEQUATE
14. **Circular imports**: S2 — 1 layer ✓ ADEQUATE
15. **Feature flag staleness**: S10 lifecycle (owner, type, removal window) — 1 layer ✓ ADEQUATE

### LOW (style, conventions)
16. **Bad naming**: S3 Naming — detailed examples per category ✓ EXTENSIVELY COVERED
17. **Wrong commit message format**: S1 Conventional Commits — detailed format spec ✓ EXTENSIVELY COVERED
18. **File organization**: S2 File Organization — detailed tree structure ✓ EXTENSIVELY COVERED

## Asymmetry Analysis

The coverage is actually quite well-proportioned. CATASTROPHIC modes have the most layers, HIGH modes have adequate coverage, and MEDIUM/LOW modes have proportional coverage.

However, I notice one specific asymmetry worth investigating:

### Potential Finding: Stale dependency vulnerability
The document tells you HOW to evaluate dependencies before adding them (S4 framework, step 4: check last published, security issues, transitive deps). It also says to run `npm audit` or `pip audit` in the "Before Submitting" checklist (S9). And S21 CI gate says "security audit with no critical or high vulnerabilities."

**But**: There is no rule about ONGOING dependency maintenance after initial adoption. What happens 6 months later when a vulnerability is discovered in a dependency you already use? The document covers:
- Initial vetting: ✓ (S4)
- Pre-submit audit: ✓ (S9)
- CI gate: ✓ (S21)
- Ongoing monitoring/Dependabot/renovation: ✗

Is this a gap? Let me falsify.

## Falsification

**Argument FOR adding ongoing dependency monitoring:**
- A dependency you vetted 6 months ago can develop a critical CVE today
- The CI gate catches it on new PRs but not if no PRs touch that dependency
- Real-world breaches come from known vulnerabilities in unpatched dependencies (Equifax/Apache Struts)
- This is a CATASTROPHIC failure mode (security breach) with no proactive rule

**Argument AGAINST adding it:**
- This is an infrastructure/tooling concern (Dependabot, Renovate, Snyk) — the document is intentionally tool-agnostic
- S21's "security audit with no critical or high vulnerabilities" implicitly catches this on every PR
- The reopening criteria say "infrastructure prerequisites are intentionally left as project-specific ADR decisions"
- Adding "run dependency audit periodically" is vague and unenforceable — what's the cadence? Who does it? It becomes dead advice.
- The CI gate + pre-submit audit already catch vulnerabilities whenever ANY code changes are submitted

**Verdict**: The gap is real but the fix would be worse than the gap. Any meaningful rule about ongoing dependency monitoring requires:
1. Specifying a tool (violates tool-agnostic principle)
2. Specifying a cadence (would be arbitrary and unenforceable)
3. Specifying ownership (human team concern, not code standard)

The existing CI gates provide defense-in-depth: every PR runs the audit, which means vulnerabilities are caught as soon as any development activity occurs. The only scenario this misses is a dormant project with zero PRs for months — and that's a project management problem, not a code standards problem.

**REJECT**: The asymmetry exists but is not fixable within the document's constraints without adding unenforceable vague advice.

## Second Finding: Missing data integrity rule

Reviewing the CATASTROPHIC category more carefully, I notice the document doesn't address **data corruption from concurrent writes without locking**. Section 17 covers optimistic/pessimistic locking as a PATTERN, but there's no rule that says "identify which tables need concurrent write protection." The coverage is:
- Pattern exists: ✓ (S17)
- Rule saying when to apply it: partially (says "any table where concurrent updates are possible" — but that's every table with more than one writer)
- Enforcement mechanism: ✗ (no CI gate can catch this; it's a design review concern)

Again, this is not fixable — you can't enforce "think about concurrency" in a standards document. S17 provides the patterns; S25 Code Review lists what to look for. The gap is inherent in the problem domain.

## Third Finding: Request ID propagation enforcement gap

Section 8 describes Request ID propagation in detail. But unlike secrets scanning (S21 CI gate) or injection prevention (S21 CI gate), there's no enforcement mechanism for request ID propagation. This is a MEDIUM-severity concern (makes debugging harder, not a data loss risk).

However, this falls into the same category as other medium-severity items — it's a development practice that's enforced through code review (S25), not CI gates. Adding a CI gate for "every HTTP handler generates a request ID" would be overly prescriptive and implementation-dependent.

**REJECT**: Proportional to severity. Code review catches it.

## Conclusion

No actionable asymmetries found. The document's protective density is well-calibrated:
- CATASTROPHIC modes: 2-6 layers each, with CI enforcement where possible
- HIGH modes: 2-3 layers each, with process enforcement
- MEDIUM modes: 1 layer each with complete patterns
- LOW modes: 1 layer each with examples

The gaps that exist (ongoing dependency monitoring, concurrent write identification, request ID enforcement) are all either:
1. Infrastructure/tooling concerns that violate the tool-agnostic principle
2. Design judgment that can't be automated
3. Already covered by adjacent mechanisms (CI gates, code review)

## Decision: NO EDIT to CLAAAAAAUDE.md
This lens found no actionable asymmetries. The document's protective density is proportional to failure severity.
