# High-Leverage Improvement Questions

## Status: LOW INVENTORY (1 active item, approaching exhaustion)

Iteration 43 closed the Section 21 coverage threshold cross-reference gap — the same pattern as iterations 29 and 31 (CI gate items referencing their defining sections).

## Active

### 1. Audience Fitness: Cross-Language Contamination Guard
- **Priority**: Low
- **Type**: Scope qualifier
- **What**: Section 3 naming conventions don't explicitly say "follow the conventions of the project's actual language/framework." AI agents blend idioms across languages (snake_case in TypeScript, TypeScript-style class hierarchies in Python).
- **Why it might matter**: Prevents subtle convention violations where code is technically correct but stylistically wrong for the project.
- **Why it might not**: The document already says "follow existing project conventions" implicitly through S9 step 5 ("every new file verify it belongs in the right directory per the architecture rules") and S11's bright line. Adding explicit language-convention matching adds words for a minor problem. Most linters catch case convention violations.
- **Estimated cost**: ~25 words
- **Leverage**: Low — linters catch the common cases; the remaining edge cases are rare

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

## Graveyarded Items
- Section 14 compression (27 words, below threshold) — evidence/section14-assessment.md
- GraphQL standards (technology-specific, violates language-agnostic principle) — graveyard.md
- Monorepo guidance (too opinionated, better as ADR per project) — graveyard.md
- Language-specific subsections (pre-seeded rejection)
- Framework-specific patterns (pre-seeded rejection)
- IDE-specific recommendations (pre-seeded rejection)

## Remaining Low-Severity Observations (Not Worth Editing)
Carried from iterations 38-43:
- `console.error` in Section 4 startup example is a legitimate pre-logger exception
- "Never name anything Handler" wording is broader than intent (refers to classes, not directories)
- Performance budgets (S7) duplicate SLO targets (S18) — same numbers, different contexts
- `revert` semver mapping compressed to "all others=no bump" — technically imprecise but acceptable
- `utils/` directory (S2) vs "never vague names like utils.ts" (S3) — file vs directory distinction
- Idempotency/backoff concepts appear in multiple sections — appropriate contextual repetition
- "zero-downtime deployments" phrase not in cited Sections 10/21 (concept present, exact term not)
- ~~Section 21 coverage enforcement doesn't cite Section 5 thresholds~~ → Fixed iteration 43
- Section 11 dependency ask doesn't cite Section 4 framework (different concerns: communication vs evaluation)
- Test name uses "and" which Section 1 flags as splitting signal (philosophical, not practical)
- Hotfix test deferral gap with "no regression test" anti-pattern (implicit resolution)
- Human-team-specific rules (S25 review turnaround, S26 incident response times, S22 rotation schedules) are dead weight for AI consumer but harmless

## Document Maturity Assessment

The document has been through 23 improvement iterations. All content-level lenses are exhausted. New meta-lenses (audience fitness, low-severity re-evaluation) have been applied. Cross-reference integrity between CI gates and their defining sections is now complete.

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

## Reopening Criteria

Future iterations would only be justified if:
1. A new failure mode is discovered in production that the current standards don't prevent
2. A new industry standard emerges (like RFC 9745 prompted the deprecation lifecycle)
3. The codebase adopts a technology that requires new universal standards (not technology-specific ones)
4. A user reports genuine ambiguity in applying the standards to a real scenario
5. A new AI agent failure mode is identified that the verify-before-generating rule doesn't cover
