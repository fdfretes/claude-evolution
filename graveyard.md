# Rejected Improvements

## Why Track This?
Prevents future iterations from rediscovering dead ends.
Each rejection must include reasoning and evidence.

---

## Pre-Seeded Rejections (from planning phase)

### Language-Specific Subsections
- **What**: Add TypeScript-specific, Python-specific, Go-specific subsections
- **Why rejected**: Document must remain language-agnostic. Principles apply across languages. Language-specific guidance belongs in separate documents.
- **Evidence**: Core thesis of CLAUDE.md is universal engineering principles
- **Alternative**: Use language-agnostic examples that translate clearly

### Framework-Specific Patterns
- **What**: Add React patterns, Django patterns, Express patterns, etc.
- **Why rejected**: Frameworks change, principles endure. Framework-specific advice becomes stale and creates maintenance burden.
- **Evidence**: Document lifespan should exceed any framework's popularity
- **Alternative**: Teach architectural patterns that work in any framework

### IDE-Specific Recommendations
- **What**: Add VSCode extensions, JetBrains settings, vim configurations
- **Why rejected**: Tool-agnostic principles are more valuable. IDE wars are unproductive.
- **Evidence**: Engineering teams use diverse tooling
- **Alternative**: Focus on outcomes (type checking, linting) not tools

---

## Iteration 37 Rejections

### Section 14 Compression
- **What**: Compress Section 14 (Database and Data Modeling) by removing redundant phrasing
- **Why rejected**: Only ~27 words recoverable (6.4%) across 3 edits. Below the cost-benefit threshold. Previous compression passes yielded 380, 325, 115, 57 words — the diminishing returns curve (now at 27) has reached the floor. Each edit risks information loss for ~6 words of savings.
- **Evidence**: evidence/section14-assessment.md
- **Alternative**: Declare Section 14 at its compression floor. No edit needed.

### GraphQL Standards
- **What**: Add GraphQL-specific standards to Section 13 (API Design)
- **Why rejected**: Technology-specific guidance violates the document's language-agnostic principle. Would add 200+ words for a pattern not every project uses. The architectural principles (schema design, N+1 prevention via dataloader, pagination) are already covered by existing sections (REST conventions, Section 7 N+1 detection, pagination contracts). GraphQL-specific guidance belongs in an ADR when a project adopts GraphQL, not in a universal standards document.
- **Evidence**: Consistent with pre-seeded rejections of framework-specific and language-specific content
- **Alternative**: Use Section 19 (ADR) to document GraphQL adoption decisions per project

### Monorepo vs Polyrepo Guidance
- **What**: Add guidance on when to use monorepo vs polyrepo structure
- **Why rejected**: Highly opinionated area with valid arguments on both sides. The decision depends on team size, deployment model, and tooling — factors that vary per organization. A universal standard cannot meaningfully prescribe this. The document already provides the decision framework: Section 19 (ADR) exists precisely for this class of project-specific architectural decision.
- **Evidence**: No industry consensus exists; Google uses monorepo, Amazon uses polyrepo, both are successful
- **Alternative**: Use Section 19 (ADR) to document repo structure decisions per project

---

## Iteration 44 Rejections

### Cross-Language Contamination Guard
- **What**: Add a rule to Section 3 saying "follow the naming conventions of the project's actual language/framework" to prevent AI agents blending idioms (snake_case in TypeScript, TypeScript-style classes in Python)
- **Why rejected**: Low leverage for ~25 words. Linters catch the common cases (case convention violations). The remaining edge cases are rare. The document already implicitly covers this through S9 step 5 ("every new file verify it belongs in the right directory per the architecture rules") and S11's bright line principle (conforming to existing patterns is silent)
- **Evidence**: Carried on frontier as low-priority since iteration 41; assessed as below editing threshold across 3 iterations
- **Alternative**: Rely on linters and existing "follow project conventions" guidance

---

## Iteration 50 Rejections

### Emergency Hotfix Schema Exception
- **What**: Add guidance to Section 12 Emergency Hotfix Protocol for when the bug IS the schema (active data corruption requiring immediate migration), bypassing Section 14's 4-phase zero-downtime migration
- **Why rejected**: The sub-case (active data corruption requiring immediate schema change) is rare — one-in-a-hundred hotfixes. The existing hotfix protocol already says "Do not attempt complex fixes under pressure" and "apply the SMALLEST possible fix" which implicitly covers: do whatever stops the bleeding. Adding explicit guidance would add ~40 words for a narrow edge case.
- **Evidence**: evidence/constraint-stacking-composability.md (Scenario 1)
- **Alternative**: Rely on the existing hotfix protocol's "smallest fix" + "disable the feature" guidance; teams facing active data corruption will make the judgment call

### Feature Flag + Multi-Phase Migration Timing
- **What**: Define when the 30-day release flag removal window starts for migration-coupled flags (Phase 1 vs Phase 3), and establish that migration phases proceed independently of flag state
- **Why rejected**: The scenario (feature flag + multi-phase zero-downtime migration simultaneously) is narrow enough that it belongs in a project-specific ADR (per S19) rather than universal standards. The correct answer depends on migration tooling, flag infrastructure, and data model — factors that vary per project. Adding guidance would add ~60 words for a scenario requiring significant project-specific context.
- **Evidence**: evidence/constraint-stacking-composability.md (Scenario 5)
- **Alternative**: Use Section 19 (ADR) to document migration-flag interaction strategy per project
