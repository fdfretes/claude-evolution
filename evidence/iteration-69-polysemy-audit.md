# Iteration 69: Polysemy Audit (Semantic Drift Across Sections)

## Lens
Do any terms in CLAAAAAAUDE.md carry different meanings in different sections, creating risk of misinterpretation?

## Distinction from Prior Lenses
- **Terminology consistency (iteration 45):** Verified named concepts use canonical names (e.g., "Pre-Commit Protocol" not "pre-commit verification protocol"). That's naming, not meaning.
- **Cross-section alignment (iterations 29, 43):** Verified numeric values and constraints align. That's quantitative, not semantic.
- **Cross-format consistency (iteration 52):** Verified data formats (JSON keys, log fields). That's format, not semantics.
- **Polysemy audit (this iteration):** Does the same word mean different things in different sections?

## Method
Audited 20 terms that appear across multiple sections. Classified each as CONSISTENT (same meaning), CONTEXTUAL (different meanings but context disambiguates), or AMBIGUOUS (risk of misinterpretation).

## Results

| Term | Classification | Sections | Risk |
|------|---------------|----------|------|
| boundary | CONTEXTUAL | 2,3,5,6,12,23 | Low |
| contract | CONTEXTUAL | 5,6,13 | Low |
| adapter | CONSISTENT | 2,4,5,10 | None |
| handler | CONSISTENT | 2,3,6,12,24 | None |
| validation | CONSISTENT | 3,4,6,12,23 | None |
| **scope** | **AMBIGUOUS** | 1,5,11,12,14 | Moderate |
| context | CONTEXTUAL | 3,6,8,10,12 | Low |
| pipeline | CONTEXTUAL | 10,12,21,23 | Low |
| lifecycle | CONSISTENT | 10,13,24 | None |
| layer | CONTEXTUAL | 2,3,12,16,21 | Low |
| module | CONSISTENT | 2,7,12,20 | None |
| interface | CONTEXTUAL | 1,2,3,9,10 | Low |
| pattern | CONTEXTUAL | 2,4,6,7,12,15,16,17,20,21 | Low |
| trust | CONTEXTUAL | preamble,3,5,6,9,12 | Low |
| **schema** | **AMBIGUOUS** | 1,2,3,4,6,14,23,24 | Moderate |
| envelope | CONTEXTUAL | 8,13 | Low |
| **protocol** | **AMBIGUOUS** | 1,11,12,20,23 | Moderate |
| service | CONTEXTUAL | 2,5,10,15,18,23 | Low |
| consumer | CONTEXTUAL | 2,13,15,23,24 | Low |
| factory | CONTEXTUAL | 2,5,6 | Low |

**8 CONSISTENT, 9 CONTEXTUAL, 3 AMBIGUOUS**

## AMBIGUOUS Findings

### 1. "Protocol" — Section 11 title vs Section 23 technical usage
- Section 11: "COMMUNICATION PROTOCOL" = rules for AI-user interaction (ask vs. silent)
- Section 23: "Communication protocol" = MQTT/HTTP/WebSocket network protocols
- Sections 1,12,20: "protocol" = procedural checklist (pre-commit protocol, hotfix protocol)
- Three distinct meanings with identical phrasing in Sections 11 and 23

### 2. "Schema" — database vs validation vs message format
- Section 14: Database schema (tables, columns, migrations)
- Sections 3,4,6: Validation schema (Zod/Joi runtime rules)
- Sections 23,24: Message schema (IoT/WebSocket payload format)
- Section 1 commit ordering says "schema type interface changes" without specifying which kind
- Section 2 models/ includes "schemas" alongside types — which kind?

### 3. "Scope" — git vs project-management vs database ORM
- Section 1: Conventional Commit scope label; staged file scope
- Sections 5,12: Project-management scope creep
- Section 14: "default scope or view" = database ORM default query filter

## Falsification

### Finding 1 (Protocol): Below editing threshold
The document's primary audience is an AI agent reading all sections into context simultaneously (confirmed iteration 64). The AI won't navigate by section headers — it reads inline, and "Section 11 COMMUNICATION PROTOCOL" is immediately followed by content about AI-user interaction rules. Section 23's "Communication protocol" is immediately followed by "use MQTT." The disambiguation is instantaneous for the primary audience. This is the same human-format concern pattern rejected in iteration 64.

### Finding 2 (Schema): Below editing threshold
Section 1's "schema type interface changes" in commit ordering is ambiguous, but the practical result is correct regardless: all structural/type-level changes (database schema, TypeScript types, validation schemas) logically precede business logic implementation. An AI placing any of these in commit 2 produces correct ordering. The ambiguity doesn't produce incorrect behavior.

### Finding 3 (Scope): Below editing threshold
Section 14's "default scope or view" could confuse non-ORM users, but "or view" immediately provides the database-native equivalent. The disambiguation is in-line and sufficient.

## Decision
**REJECT** — All 3 AMBIGUOUS findings are below the editing threshold:
- Finding 1: Human-format concern irrelevant for AI audience (same pattern as iteration 64)
- Finding 2: Ambiguity doesn't produce incorrect behavior
- Finding 3: In-line "or view" qualifier already disambiguates

## Observations
- Of 20 terms audited, 85% (17/20) are either fully CONSISTENT or clearly CONTEXTUAL
- The 3 AMBIGUOUS terms are all disambiguated by immediate context for the primary audience
- This confirms the document's writing style effectively uses qualifying phrases to prevent semantic drift
- The "protocol" dual-usage (Section 11 vs 23) is the single most confusing polysemy but is addressed by the fact that AI agents don't scan headers in isolation
