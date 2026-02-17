# High-Leverage Improvement Questions

## Status: EXHAUSTED (0 active items)

Iteration 45 applied a forward-reference and terminology audit lens, finding 2 fixable issues (both resolved). No new active items emerged.

## Active

(none)

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
- ~~Contradiction: "No any ever" vs "without justification"~~ → Fixed iteration 40
- ~~Audience Fitness: Verify Before Generating~~ → Added iteration 41
- ~~Self-contradiction: "No boolean parameters" bans its own solution~~ → Fixed iteration 42
- ~~Cross-reference: Section 21 coverage thresholds don't cite Section 5~~ → Fixed iteration 43
- ~~Numeric constraint consistency~~ → Verified clean iteration 44
- ~~Actionability audit~~ → Verified clean iteration 44
- ~~Cross-Language Contamination Guard~~ → Graveyarded iteration 44
- ~~Forward reference: S7 cursor pagination delegates to S13 with no definition~~ → Fixed iteration 45
- ~~Terminology: "pre-commit verification protocol" vs "Pre-Commit Protocol"~~ → Fixed iteration 45

## Graveyarded Items
- Section 14 compression (27 words, below threshold) — evidence/section14-assessment.md
- GraphQL standards (technology-specific, violates language-agnostic principle) — graveyard.md
- Monorepo guidance (too opinionated, better as ADR per project) — graveyard.md
- Language-specific subsections (pre-seeded rejection)
- Framework-specific patterns (pre-seeded rejection)
- IDE-specific recommendations (pre-seeded rejection)
- Cross-language contamination guard (low leverage, linters catch common cases, ~25 words for rare edge case) — graveyard.md

## Remaining Low-Severity Observations (Not Worth Editing)
Carried from iterations 38-45:
- `console.error` in Section 4 startup example is a legitimate pre-logger exception
- "Never name anything Handler" wording is broader than intent (refers to classes, not directories)
- Performance budgets (S7) duplicate SLO targets (S18) — same numbers, different contexts
- `revert` semver mapping compressed to "all others=no bump" — technically imprecise but acceptable
- `utils/` directory (S2) vs "never vague names like utils.ts" (S3) — file vs directory distinction
- Idempotency/backoff concepts appear in multiple sections — appropriate contextual repetition
- "zero-downtime deployments" phrase not in cited Sections 10/21 (concept present, exact term not)
- Section 11 dependency ask doesn't cite Section 4 framework (different concerns: communication vs evaluation)
- Test name uses "and" which Section 1 flags as splitting signal (philosophical, not practical)
- Hotfix test deferral gap with "no regression test" anti-pattern (implicit resolution)
- Human-team-specific rules (S25 review turnaround, S26 incident response times, S22 rotation schedules) are dead weight for AI consumer but harmless
- S3 Graceful Shutdown forward-references S10/S21 (MEDIUM, but rule is self-contained without the cross-reference)
- Unlabeled preamble referenced as "the preamble" in S10 (LOW, obvious from context)

## Document Maturity Assessment

The document has been through 25 improvement iterations. All content-level and meta-level lenses are exhausted. The frontier is empty.

| Lens | Iterations | Status |
|------|-----------|--------|
| Contradictions | 21, 40 | Exhausted (0 remaining) |
| Gap fills | 22, 27, 28, 30 | Exhausted (all mechanisms connected) |
| Compressions | 23, 25, 35, 36, 37 | Exhausted (at floor) |
| Boundary delineation | 24 | Exhausted (all overlaps resolved) |
| Scope qualifiers | 26 | Exhausted (all ambiguities clarified) |
| Cross-section alignment | 29, 43 | Exhausted (all inconsistencies fixed) |
| Example-to-rule promotion | 30 | Exhausted (implicit patterns made explicit) |
| Rule-to-gate connection | 31, 32 | Exhausted (all absolute rules enforced) |
| Mechanism gap fills | 33, 34 | Exhausted (all lifecycles complete) |
| Symmetric coverage | 30 | Exhausted (input/output both covered) |
| Enforcement audit | 31, 32 | Exhausted (all rules verified in CI) |
| Self-contradiction audit | 38, 42 | Exhausted (examples comply with rules) |
| Cross-reference integrity | 39, 43 | Exhausted (references verified, CI gates cite sources) |
| Audience fitness | 41 | Applied (1 HIGH fix; remaining items low-leverage) |
| Low-severity re-evaluation | 42, 43 | Applied (2 fixes from 13 items; remainder confirmed below threshold) |
| Numeric constraint consistency | 44 | Applied (0 findings — all thresholds compatible) |
| Actionability audit | 44 | Applied (0 findings — action specs appropriately detailed) |
| Forward reference & terminology | 45 | Applied (2 fixes — inline definition + name alignment) |

## Reopening Criteria

Future iterations would only be justified if:
1. A new failure mode is discovered in production that the current standards don't prevent
2. A new industry standard emerges (like RFC 9745 prompted the deprecation lifecycle)
3. The codebase adopts a technology that requires new universal standards (not technology-specific ones)
4. A user reports genuine ambiguity in applying the standards to a real scenario
5. A new AI agent failure mode is identified that the verify-before-generating rule doesn't cover
6. A genuinely novel audit lens is identified that hasn't been applied
