# Scope Boundary Audit — Iteration 55

## Lens Description
Check whether absolute rules have unstated scope boundaries — legitimate edge cases where literal application would be counterproductive.

## Methodology
Extracted all rules using "every," "always," "never," "must," "max," "no" and tested each against common, legitimate scenarios where literal application produces a worse outcome than violation.

## Findings: 3 HIGH, 14 MEDIUM

### Applied (3 HIGH-severity edits)

**Finding 1: "Every table has created_at and updated_at" (S14)**
- Edge case: Pure join tables (user_roles, post_tags) have no independent lifecycle. `updated_at` is meaningless — rows are inserted or deleted, never updated.
- Fix: Scoped to "entity table" and noted join tables need only `created_at`. +14 words.

**Finding 2: "Max 300 lines per file" (S2)**
- Edge case: Auto-generated files (Prisma clients, OpenAPI types), migration files that create multiple tables atomically, large declarative schema files — cannot be meaningfully split.
- Fix: Scoped to "hand-written source file" with generated/migration exemption. +9 words.

**Finding 3: "One exported concept per file" (S2)**
- Edge case: Type definition files in models/ naturally group related types (Order, OrderLine, OrderStatus, CreateOrderInput). Splitting each into its own file creates unnecessary proliferation.
- Partial escape hatch existed: models/ directory described as "types interfaces schemas enums" implying grouping, but the universal rule contradicted this.
- Fix: Added explicit exception for type files in models/. +22 words.

### Not Applied (14 MEDIUM-severity, below editing threshold)

1. **Never use raw literals in tests (S5)**: Factory functions are overkill for primitive-input pure function tests like `slugify("Hello World")`. But practitioners would naturally apply judgment. LOW in practice.

2. **Never SELECT * (S7)**: ORM full-entity loads are effectively SELECT all-defined-columns. The "production queries" qualifier plus existing iteration 38 fix (enumerating columns in examples) is sufficient.

3. **Default soft deletes (S14)**: GDPR right-to-erasure conflicts. But anonymize-then-soft-delete is the standard pattern, and project-specific legal compliance is an ADR (S19) concern.

4. **Every bug fix ships with regression test (S5, S12)**: Environment-specific bugs can't always be reproduced in test. But Phase 1's "cannot reproduce" checklist + Emergency Hotfix Protocol's deferred test writing provide sufficient escape path.

5. **Max 30 lines per function (S3)**: Flat dispatchers and field mappers may exceed 30 lines while being trivially simple. But practitioners would naturally apply judgment ("extract sub-functions with descriptive names that serve as documentation" is the spirit).

6. **Migrations must be reversible (S14)**: "If a migration cannot be reversed document why" already provides the escape hatch. The word "must" followed immediately by the exception is a clarity issue but not harmful.

7. **core/ zero external packages (S2)**: Pure computational libraries (decimal.js for financial math) arguably belong in core/. But wrapping behind an adapter interface is the existing pattern — core defines the interface, adapters provide the implementation.

8. **TODO contradiction (S1 Law 4 vs S11)**: Law 4 says "never commit TODO hacks" while S11 says "without ticket reference." Reconcilable through careful reading: "TODO hacks" as compound noun + Step 4's "evaluate if intentional." Below editing threshold.

9. **Every handler validates with schema (S6)**: Internal event handlers consuming trusted messages. But defense-in-depth at boundaries is the document's core security principle. Internal trust is dangerous.

10. **Every service exposes GET /health (S10)**: Background workers have no HTTP server. But the document context is web services; workers are implicitly exempt. Adding non-HTTP health patterns would add ~30 words for an edge case.

11. **UUIDs for public-facing IDs (S14)**: Constrained IoT devices. But the rule says "public-facing IDs" — device-internal IDs are not public-facing. Existing scope is sufficient.

12. **Validate messages on both sides (S23)**: ESP32 can't run full schema validation. But "validate" doesn't require Zod — basic field presence and range checks count.

13. **No reproduction = no fix attempt (S12)**: Security vulnerabilities with undeniable evidence. But Emergency Hotfix Protocol's "disable the broken feature" is the escape hatch. The prohibition is against speculative code changes, not against defensive boundary tightening.

14. **PRs over 400 lines (S25)**: Test-only PRs may exceed this. But "meaningful changes" qualifier provides latitude. Test code is lower-risk per line.

## Falsification

**Would these edits make anything worse?**
- Finding 1: Could someone abuse "pure join table" to skip timestamps on tables that should have them? No — the qualifier "only foreign keys" is clear. If a join table carries additional data, it's an entity table.
- Finding 2: Could someone abuse "auto-generated" to claim their 500-line hand-written file is "practically generated"? Unlikely — "auto-generated files and migration files" is specific enough.
- Finding 3: Could someone abuse "cohesive group of related types" to put everything in one file? The constraint "for one domain concept" and the existing 300-line limit (now scoped) provide guardrails.

**Do these edits contradict other sections?**
- No. All three narrow an absolute rule by adding a scope qualifier for a specific, well-defined case.

## Net Impact
+45 words across 3 edits. All three scope absolute rules to prevent literal misapplication in common scenarios.
