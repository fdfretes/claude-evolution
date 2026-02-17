# High-Leverage Improvement Questions
Ranked by: How much would answering this improve CLAAAAAAUDE.md?

## Priority 1 (Low-Medium Leverage — Diminishing Returns Territory)

### 1. Missing: GraphQL Standards
- **Issue**: REST is thoroughly covered in Section 13, GraphQL mentioned but not specified
- **Questions**: When to use GraphQL vs REST? Schema design? N+1 query prevention (dataloader)?
- **Leverage**: LOW-MEDIUM - affects API design decisions in GraphQL projects
- **Impact**: Completes API design coverage
- **Risk**: Could add 200+ words for a pattern not every project uses. May belong in an ADR template rather than a universal standard.

### 2. Missing: Monorepo vs Polyrepo Guidance
- **Issue**: No guidance on when to split repos or use monorepo
- **Questions**: When is monorepo appropriate? When to split? Tooling standards?
- **Leverage**: LOW-MEDIUM - affects project structure decisions
- **Risk**: Highly opinionated area. May be better as an ADR template than a hard rule.

## Priority 2 (Low Leverage)

### 3. Enhancement: Concrete Zod Schema Examples
- **Issue**: Section 6 mentions Zod but no concrete patterns shown
- **Leverage**: LOW - helpful but not critical

### 4. Clarity: Soft Delete Implementation Details
- **Issue**: Section 14 says "default to soft deletes" but minimal implementation guidance
- **Leverage**: LOW - most teams figure this out

## Document Maturity Assessment

The document has been through 14 improvement iterations (21-34). All high-severity issues are resolved:
- All contradictions fixed (iterations 21, 24)
- All critical gaps filled (iterations 22, 27, 28, 30, 33, 34)
- Two major compression passes complete (iterations 23, 25)
- Edge case ambiguities clarified (iteration 26)
- Cross-section inconsistencies resolved (iteration 29)
- Security model symmetric: input validation + output serialization (iteration 30)
- All absolute rules connected to CI enforcement (iterations 31, 32)
- API lifecycle complete: creation → versioning → deprecation → removal (iteration 33)
- Feature flag lifecycle complete: types → ownership → cleanup → name safety (iteration 34)

**The document has reached comprehensive maturity.** All remaining items are low-leverage additions that would expand scope rather than improve quality. Future iterations should focus on:
1. Discovering genuinely novel gaps via new analysis lenses
2. Compression opportunities (the document is ~11,600 words)
3. Moving low-leverage items to graveyard if they fail cost-benefit analysis

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
- ~~Missing: Feature Flag Lifecycle~~ → Added iteration 34

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
- Compression pass: can any section be tightened further without information loss?
