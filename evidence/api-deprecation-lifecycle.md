# API Deprecation Lifecycle - Evidence (Iteration 33)

## Problem
Section 13 says "support the previous version for at least 6 months after deprecation notice" but never defines:
1. What constitutes a deprecation notice
2. How to communicate to consumers
3. What headers to return
4. When removal is safe
5. What status code after sunset

## Real Failure Scenarios
1. **Silent removal**: Developer removes /api/v1 after 8 months. No headers returned. Three clients break at 2am.
2. **Ambiguous notice**: Team posts in Slack "v1 deprecated." Partner team not in channel has production incident at removal.
3. **Unmonitored shutdown**: Sunset headers returned, 6 months pass, endpoint removed. Three services never migrated because nobody checked traffic.
4. **Confusing 404**: Endpoint removed, client gets 404, developer spends hours debugging "routing issue." 410 Gone with Link header would be a 5-minute fix.

## Standards Basis
- **RFC 9745 (March 2025)**: Deprecation HTTP Response Header Field — `Deprecation: @1688169599`
- **RFC 8594 (May 2019)**: Sunset HTTP Header Field — `Sunset: Sun, 30 Jun 2024 23:59:59 UTC`
- Both are IETF standards (not proposals)

## Key Design Decisions

### Why not bundle feature flag cleanup?
Separate concerns:
- API deprecation = external contract lifecycle (consumers outside your codebase)
- Feature flag cleanup = internal code hygiene (your own codebase)
Feature flag cleanup deferred to separate future iteration.

### Why remove "6 months" from new text?
Already stated in the preceding sentence. Repeating would violate DRY.

### Why "zero traffic for 30 days"?
Safety gate preventing removal while consumers are still calling. Monitoring is the enforcement mechanism (also stated in the text).

### Why 410 Gone not 404?
410 is semantically correct (resource existed but was intentionally removed). Combined with Link header, it gives consumers actionable information. 404 causes wasted debugging time.

## Falsification
1. **Does it contradict existing sections?** No. Section 8 already lists "deprecated API called" as warn-level.
2. **Does it duplicate?** No. The "6 months" clause was intentionally omitted since it's already stated.
3. **Is it organization-specific?** No. RFC headers are universal HTTP semantics.
4. **Could it be an ADR template instead?** No. It's a repeatable process, not a one-time decision.
5. **Word count?** ~85 words. Within the 80-100 budget.

## Cross-References
- Section 8: warn level for deprecated API calls (existing)
- Section 13: API versioning paragraph (existing, extended)
