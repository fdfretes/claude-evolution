# High-Leverage Improvement Questions

## Status: TERMINAL (confirmed at iterations 56-65)

Iteration 55 declared frontier exhausted. Iterations 56-64 independently verified via 9 distinct approaches (4 candidate lenses, fresh-eyes, data invariant depth, end-to-end simulation, adversarial compliance, partial adoption safety, misapplication recovery, temporal obsolescence, cognitive load under stress). Iteration 65 evaluated 3 final candidate lenses (instruction stability under context compression, composability with external tooling, multi-agent coordination) — all rejected as not addressable by document edits, subsumed by prior lenses, or outside scope. Protocol has reached terminal state.

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
- ~~Temporal ordering: Phase 4 regression test commit violates Law 1 bisect-safety~~ → Fixed iteration 46
- ~~Missing negative guidance: merge conflict markers not in contamination scan~~ → Fixed iteration 47
- ~~Prerequisite: Feature flag implementation pattern missing~~ → Added iteration 48
- ~~Failure mode asymmetry: protective density proportional~~ → Verified clean iteration 49
- ~~Constraint stacking: S20 refactoring-reveals-bug deadlock with S12/S5~~ → Fixed iteration 50
- ~~Error recovery path completeness: procedure failure branches~~ → Verified clean iteration 51
- ~~Cross-format consistency: JSON key convention and mixed S8 example~~ → Fixed iteration 52
- ~~Trust boundary transitions: data flow boundary coverage~~ → Verified clean iteration 53
- ~~Rule verifiability: absolute rules calibrated to verification mechanism~~ → Verified clean iteration 54
- ~~Scope boundaries: join table timestamps, generated file limit, type file export~~ → Fixed iteration 55
- ~~Frontier exhaustion verification~~ → Confirmed iteration 56
- ~~Fresh eyes verification: AI behavioral correctness, defense-in-depth, low-severity promotion~~ → Reconfirmed iteration 57
- ~~Data invariant enforcement depth: database-level CHECK constraints~~ → Rejected (derivable from trust boundary coverage) iteration 58
- ~~End-to-end scenario simulation: 4 multi-section practitioner walkthroughs~~ → Verified correct iteration 59
- ~~Adversarial compliance testing: 10 letter-vs-spirit gaming scenarios~~ → Verified resistant iteration 60
- ~~Partial adoption safety: 5 section-isolation decomposition scenarios~~ → Verified safe iteration 61
- ~~Misapplication recovery: 8 honest-mistake feedback loop scenarios~~ → Verified adequate iteration 62
- ~~Temporal obsolescence resilience: 14 technology references, 6 paradigm areas~~ → Verified resilient iteration 63
- ~~Cognitive load under stress: 5 high-pressure scenarios, decision path efficiency~~ → Verified optimized for AI consumer iteration 64
- ~~Terminal state assessment: instruction compression stability, external tooling composability, multi-agent coordination~~ → All rejected, protocol terminal iteration 65

## Graveyarded Items
- Section 14 compression (27 words, below threshold) — evidence/section14-assessment.md
- GraphQL standards (technology-specific, violates language-agnostic principle) — graveyard.md
- Monorepo guidance (too opinionated, better as ADR per project) — graveyard.md
- Language-specific subsections (pre-seeded rejection)
- Framework-specific patterns (pre-seeded rejection)
- IDE-specific recommendations (pre-seeded rejection)
- Cross-language contamination guard (low leverage, linters catch common cases, ~25 words for rare edge case) — graveyard.md
- Ongoing dependency monitoring (tool-specific, cadence unenforceable, CI gates provide defense-in-depth) — evidence/failure-mode-asymmetry-audit.md
- Emergency hotfix schema exception (rare sub-case, existing "smallest fix" guidance sufficient) — graveyard.md
- Feature flag + multi-migration timing (niche, better as project-specific ADR) — graveyard.md

## Remaining Low-Severity Observations (Not Worth Editing)
Carried from iterations 38-64 (unchanged — no promotions at iterations 56-64):
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
- Zero-downtime migration phases lack explicit inter-phase verification gates (derivable from Phase 4's existing "after confirming" pattern)
- Emergency hotfix defers regression test with no merge-gate deadline (temporal window exists but hotfix protocol is inherently exception-based)
- Refactoring prerequisite tests must be separate PR (derivable from intersection of Law 2 + S20 Step 5)
- `json_agg(o.*)` in Section 7 N+1 example uses `*` inside aggregate (idiomatic PostgreSQL, not top-level SELECT *)
- CI tooling for injection scanning and architecture verification is intentionally tool-agnostic (grep patterns provided for local workflow; specific tools are technology-dependent)
- Infrastructure prerequisites (MQTT broker, time-series DB, monitoring platform, secrets manager) are intentionally left as project-specific ADR decisions
- Redis optional-vs-required ambiguity across sections (config marks optional, scaling sections assume present — context-dependent, not contradictory)
- Structured logger library selection is covered by Section 4 dependency framework
- Cross-layer bug fix commit scoping (Law 1 bisect-safety serves as tiebreaker for Law 2 when splitting would break intermediate commits) — derivable, not worth explicit text
- S9 step 2→3 has no explicit "if existing solution found, stop" gate (derivable from "must not reinvent what exists")
- S12 Phase 4 "three commits minimum" is conditional on Phase 3 finding similar patterns (derivable from context)
- S22 JWT overlap period has no duration guidance (narrow operational detail, ~15 words)
- S15 retry exhaustion has no explicit "what next" (derivable from error handling architecture)
- ISO 8601 timestamp format only explicitly stated for WebSocket (S24) — implied universally by UTC mandate + S3 gotcha example + S14 timestamptz
- MQTT schema (S23) uses flat field list vs WebSocket (S24) nested object — correct protocol-boundary divergence
- Health check envelope (S10) doesn't use API `{ data }` envelope (S13) — correct, infrastructure vs API endpoint
- Outbound HTTP request construction (SSRF prevention) not explicitly stated — derivable from injection prevention pattern + adapter architecture
- "One logical assertion per test" uses judgment word "logical" — correctly self-scoping as heuristic (iteration 54 finding)
- "Never hold a database lock while making an external HTTP call" requires cross-function path analysis — correctly absolute despite verification difficulty (iteration 54 finding)
- TODO contradiction between S1 Law 4 ("never commit TODO hacks") and S11 ("without ticket reference") — reconcilable: "TODO hacks" as compound noun + Step 4 "evaluate if intentional" (iteration 55 finding)
- "Never use raw literals in tests" is overkill for primitive-input pure function tests — practitioners naturally apply judgment (iteration 55 finding)
- "Max 30 lines per function" for flat dispatchers/mappers — practitioners recognize trivially-simple line exceptions (iteration 55 finding)
- "Every service exposes GET /health" doesn't address non-HTTP workers — implicit scope to HTTP services (iteration 55 finding)
- "No reproduction means no fix attempt" could block defensive measures against undeniable security evidence — Emergency Hotfix Protocol provides escape (iteration 55 finding)
- Database-level CHECK constraints for business invariants not explicitly mentioned — derivable from "validate at boundaries" + database as trust boundary (iteration 58 finding)
- Hand-rolled redundant validation in core/ not explicitly prohibited — derivable from "typed and trusted" + core purity principle (iteration 62 finding)
- Non-failing regression test depends on per-commit CI or reviewer discipline — Phase 4 structure is correct defense; CI-specifics are tool-dependent (iteration 62 finding)
- S22 rotation cadences (90/180/365 days) may age as industry shifts toward shorter windows — principle "every secret has a rotation schedule" is durable; numbers are starting defaults (iteration 63 finding)
- S7 performance budget numbers (200ms/500ms/50ms) will shift with hardware — "profile and optimize if exceeded" is the real rule (iteration 63 finding)
- Client-server assumption in S2 handler pattern — already extended with "CLI commands event consumers WebSocket handlers" (iteration 63 finding)
- S12/S26 have no cross-reference for incident handling — each self-contained for its concern; AI consumer sees both simultaneously (iteration 64 finding)
- Merge conflict resolution guidance is minimal (11 words) — deliberately judgment-dependent, conflict resolution is context-specific (iteration 64 finding)
- S12 Decision tree placed at end of section after 1,000+ words — irrelevant for AI consumer; valid concern for hypothetical human reader (iteration 64 finding)

## Document Maturity Assessment

The document has been through 44 improvement iterations. All content-level and meta-level lenses are exhausted. Frontier exhaustion independently verified at iterations 56, 57, 58, 59, 60, 61, 62, 63, 64, and 65.

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
| Implicit temporal ordering | 46 | Applied (1 fix — regression test squash note resolves Phase 4 vs Law 1) |
| Missing negative guidance | 47 | Applied (1 fix — merge conflict markers added to contamination scan) |
| Prerequisite chain completeness | 48 | Applied (1 fix — feature flag implementation pattern; 9 others by-design or below threshold) |
| Failure mode asymmetry | 49 | Applied (0 findings — protective density proportional to severity) |
| Constraint stacking composability | 50 | Applied (1 fix — refactoring-reveals-bug deadlock; 2 graveyarded; 2 clean) |
| Error recovery path completeness | 51 | Applied (0 findings — all failure branches handled or derivable) |
| Cross-format consistency | 52 | Applied (1 fix — JSON key convention + S8 example; 6 LOW findings rejected) |
| Trust boundary transitions | 53 | Applied (0 findings — 12 boundaries audited, 11 explicit, 1 derivable) |
| Rule verifiability | 54 | Applied (0 findings — ~45 absolutes audited, all correctly calibrated) |
| Scope boundaries | 55 | Applied (3 fixes — join table timestamps, generated file limit, type file export; 14 MEDIUM rejected) |
| Frontier exhaustion verification | 56 | Confirmed (4 candidate lenses evaluated, all rejected) |
| Fresh eyes verification | 57 | Reconfirmed (AI behavioral correctness, defense-in-depth, low-severity promotion — all rejected) |
| Data invariant enforcement depth | 58 | Rejected (derivable from trust boundary coverage + boundary validation principle) |
| End-to-end scenario simulation | 59 | Verified correct (4 scenarios across 18/26 sections, all produce correct results) |
| Adversarial compliance testing | 60 | Verified resistant (10 gaming scenarios, all blocked by constraint + intent pairing) |
| Partial adoption safety | 61 | Verified safe (5 decomposition scenarios, all sections self-contained and safe in isolation) |
| Misapplication recovery | 62 | Verified adequate (8 scenarios: 3 CAUGHT, 3 PARTIALLY CAUGHT, 2 SILENT but low-severity and inherently judgment-dependent) |
| Temporal obsolescence resilience | 63 | Verified resilient (14 technology refs properly scoped, 6 paradigm areas have escape hatches, "principle + example + or equivalent" pattern throughout) |
| Cognitive load under stress | 64 | Verified optimized for primary audience (5 scenarios tested; format findings are human-specific, content findings are handled or judgment-dependent) |
| Terminal state assessment | 65 | Confirmed terminal (3 candidate lenses rejected: not document-addressable, subsumed, or out of scope) |

## Reopening Criteria

Future iterations would only be justified if:
1. A new failure mode is discovered in production that the current standards don't prevent
2. A new industry standard emerges (like RFC 9745 prompted the deprecation lifecycle)
3. The codebase adopts a technology that requires new universal standards (not technology-specific ones)
4. A user reports genuine ambiguity in applying the standards to a real scenario
5. A new AI agent failure mode is identified that the verify-before-generating rule doesn't cover
6. A genuinely novel audit lens is identified that hasn't been applied
7. The document's primary audience shifts from AI agent to human developer (would trigger format restructuring)
