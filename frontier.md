# High-Leverage Improvement Questions
Ranked by: How much would answering this improve CLAAAAAAUDE.md?

## Priority 1 (Medium Leverage — Genuine Gaps)

### 1. Missing: Feature Flag Lifecycle
- **Issue**: Section 10 says "Feature flags over long-lived feature branches" but provides zero guidance on flag types, naming, expiration, or cleanup
- **Questions**: How to distinguish release flags (temporary) from ops flags (permanent)? What's the cleanup cadence? How to prevent feature flag debt accumulation?
- **Leverage**: MEDIUM — feature flags without cleanup guidance become indefinite technical debt
- **Impact**: Prevents stale flags from accumulating (common real-world problem)
- **Risk**: ~50-60 words. Must be principles not tooling-specific. Need to distinguish from API deprecation lifecycle (external) vs flag cleanup (internal).

## Priority 2 (Low-Medium Leverage — Diminishing Returns Territory)

### 2. Missing: GraphQL Standards
- **Issue**: REST is thoroughly covered in Section 13, GraphQL mentioned but not specified
- **Questions**: When to use GraphQL vs REST? Schema design? N+1 query prevention (dataloader)?
- **Leverage**: LOW-MEDIUM - affects API design decisions in GraphQL projects
- **Impact**: Completes API design coverage
- **Risk**: Could add 200+ words for a pattern not every project uses. May belong in an ADR template rather than a universal standard.

### 3. Missing: Monorepo vs Polyrepo Guidance
- **Issue**: No guidance on when to split repos or use monorepo
- **Questions**: When is monorepo appropriate? When to split? Tooling standards?
- **Leverage**: LOW-MEDIUM - affects project structure decisions
- **Risk**: Highly opinionated area. May be better as an ADR template than a hard rule.

## Priority 3 (Low Leverage)

### 4. Enhancement: Concrete Zod Schema Examples
- **Issue**: Section 6 mentions Zod but no concrete patterns shown
- **Leverage**: LOW - helpful but not critical

### 5. Clarity: Soft Delete Implementation Details
- **Issue**: Section 14 says "default to soft deletes" but minimal implementation guidance
- **Leverage**: LOW - most teams figure this out

## Document Maturity Assessment

The document has been through 13 improvement iterations (21-33). All high-severity issues are resolved:
- All contradictions fixed (iterations 21, 24)
- All critical gaps filled (iterations 22, 27, 28, 30, 33)
- Two major compression passes complete (iterations 23, 25)
- Edge case ambiguities clarified (iteration 26)
- Cross-section inconsistencies resolved (iteration 29)
- Security model symmetric: input validation + output serialization (iteration 30)
- All absolute rules connected to CI enforcement (iterations 31, 32)
- API lifecycle complete: creation → versioning → deprecation → removal (iteration 33)

**The document's API lifecycle is now complete.** The remaining Priority 1 item (feature flag lifecycle) is an internal code hygiene concern, distinct from the external API lifecycle. Future iterations should continue applying strict cost-benefit analysis.

## Resolved
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

## Graveyard Candidates (Revisit if evidence changes)
- Adding language-specific subsections (rejected: keep language-agnostic)
- Framework-specific patterns (rejected: principles over frameworks)
- IDE-specific recommendations (rejected: tool-agnostic)
- GraphQL standards (may be better as ADR template — evaluate if demand emerges)
- Monorepo guidance (too opinionated for universal standard)

## Questions for Future Exploration
- Data transformation contracts at every layer boundary (not just response)
- WebAssembly integration standards
- Microfrontend architecture guidance
- ML model deployment patterns
