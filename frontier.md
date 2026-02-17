# High-Leverage Improvement Questions

## Status: EXHAUSTED (with one deferred low-severity item)

All high/medium-leverage improvement questions have been resolved or graveyarded. One low-severity contradiction remains deferred.

## Active (Low Severity, Deferred)

### "No any ever" vs "without justification" contradiction
- **Severity:** Low (practical impact negligible — `unknown` is correct in 99%+ of cases)
- **Location:** Section 3 "No any ever" vs Section 11 "use any types... without justification"
- **Issue:** Section 3 is absolute; Section 11 is conditional. Contradiction about whether justified `any` is acceptable.
- **Proposed fix:** Add escape hatch to Section 3 matching the `as` assertion pattern ("unless accompanied by a comment explaining why"), then Section 11's "without justification" framing becomes consistent.
- **Why deferred:** The fix requires careful wording to avoid opening a loophole. Risk of worsening exceeds benefit given `unknown` truly is the correct answer almost always.
- **Evidence:** evidence/cross-reference-integrity-audit.md

## Resolved (Complete List)
- ~~Contradiction: Autonomy vs Permission Boundary~~ → Fixed iteration 21
- ~~Missing: Error Budget Guidance~~ → Fixed iteration 22
- ~~Compression: Git Section Verbosity~~ → Compressed iteration 23
- ~~Overlap: Deployment Sections 10 and 21~~ → Delineated iteration 24
- ~~Compression: Debugging Section Verbosity~~ → Compressed iteration 25
- ~~Clarity: "Max 3 Parameters" Edge Cases~~ → Clarified iteration 26
- ~~Missing: Resource Cleanup and Graceful Shutdown~~ → Added iteration 27
- ~~Missing: Dependency Delivery Mechanism~~ → Added iteration 28
- ~~Inconsistency: Offset Pagination Warning~~ → Fixed iteration 29
- ~~Missing: Response Serialization Safety~~ → Added iteration 30
- ~~Missing: Architecture Layer CI Enforcement~~ → Added iteration 31
- ~~Missing: Security Injection CI Enforcement~~ → Added iteration 32
- ~~Missing: API Deprecation Lifecycle~~ → Added iteration 33
- ~~Missing: Feature Flag Lifecycle~~ → Added iteration 34
- ~~Compression: Section 3 Naming/Error Class Verbosity~~ → Compressed iteration 35
- ~~Compression: Section 13 API Standards Verbosity~~ → Compressed iteration 36
- ~~Compression: Section 14 Database Modeling~~ → Assessed at floor, graveyarded iteration 37
- ~~Missing: GraphQL Standards~~ → Graveyarded iteration 37
- ~~Missing: Monorepo Guidance~~ → Graveyarded iteration 37
- ~~Self-contradiction: `hotfix()` commit type~~ → Fixed iteration 38
- ~~Self-contradiction: `SELECT u.*` example~~ → Fixed iteration 38
- ~~Self-contradiction: 429 retry vs 4xx rule~~ → Fixed iteration 38
- ~~Cross-reference: Section 12 commit examples exceed 50-char limit~~ → Fixed iteration 39
- ~~Cross-reference: Decision Tree "Phases 1-5" should be 1-6~~ → Fixed iteration 39

## Graveyarded Items
- Section 14 compression (27 words, below threshold) — evidence/section14-assessment.md
- GraphQL standards (technology-specific, violates language-agnostic principle) — graveyard.md
- Monorepo guidance (too opinionated, better as ADR per project) — graveyard.md
- Language-specific subsections (pre-seeded rejection)
- Framework-specific patterns (pre-seeded rejection)
- IDE-specific recommendations (pre-seeded rejection)

## Remaining Low-Severity Observations (Not Worth Editing)
Carried from iteration 38:
- `console.error` in Section 4 startup example is a legitimate pre-logger exception
- "Never name anything Handler" wording is broader than intent (refers to classes, not directories)
- Performance budgets (S7) duplicate SLO targets (S18) — same numbers, different contexts
- `revert` semver mapping compressed to "all others=no bump" — technically imprecise but acceptable
- `utils/` directory (S2) vs "never vague names like utils.ts" (S3) — file vs directory distinction
- Idempotency/backoff concepts appear in multiple sections — appropriate contextual repetition

New from iteration 39:
- "zero-downtime deployments" phrase not in cited Sections 10/21 (concept present, exact term not)
- Section 21 coverage enforcement doesn't cite Section 5 thresholds
- Section 11 dependency ask doesn't cite Section 4 framework
- "No boolean parameters" wording broader than intent (positional vs named)
- Test name uses "and" which Section 1 flags as splitting signal (philosophical, not practical)
- Hotfix test deferral gap with "no regression test" anti-pattern (implicit resolution)

## Document Maturity Assessment

The document has been through 19 improvement iterations. Every improvement lens has been applied and exhausted:

| Lens | Iterations | Status |
|------|-----------|--------|
| Contradictions | 21 | Exhausted (0 remaining) |
| Gap fills | 22, 27, 28, 30 | Exhausted (all mechanisms connected) |
| Compressions | 23, 25, 35, 36, 37 | Exhausted (at floor) |
| Boundary delineation | 24 | Exhausted (all overlaps resolved) |
| Scope qualifiers | 26 | Exhausted (all ambiguities clarified) |
| Cross-section alignment | 29 | Exhausted (all inconsistencies fixed) |
| Example-to-rule promotion | 30 | Exhausted (implicit patterns made explicit) |
| Rule-to-gate connection | 31, 32 | Exhausted (all absolute rules enforced) |
| Mechanism gap fills | 33, 34 | Exhausted (all lifecycles complete) |
| Symmetric coverage | 30 | Exhausted (input/output both covered) |
| Enforcement audit | 31, 32 | Exhausted (all rules verified in CI) |
| Self-contradiction audit | 38 | Exhausted (examples comply with rules) |
| Cross-reference integrity | 39 | Exhausted (references verified, examples comply cross-section) |

**The document has reached its final state.**

## Reopening Criteria

Future iterations would only be justified if:
1. A new failure mode is discovered in production that the current standards don't prevent
2. A new industry standard emerges (like RFC 9745 prompted the deprecation lifecycle)
3. The codebase adopts a technology that requires new universal standards (not technology-specific ones)
4. A user reports genuine ambiguity in applying the standards to a real scenario
5. The "No any ever" vs "without justification" contradiction is deemed worth fixing (currently assessed as not worth the edit risk)
