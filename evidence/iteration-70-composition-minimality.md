# Iteration 70: Composition Minimality Lens

## Lens Definition
Are there rules in CLAAAAAAUDE.md that are strict logical consequences of other rules already present? If rule A is logically entailed by rules B + C, rule A could be removed without coverage loss, improving conciseness.

## Distinction from Prior Compression Passes
Compression iterations (23, 25, 35, 36, 37) targeted **phrasings** — redundant words, restated concepts, duplicate examples. Composition minimality targets **entire rules** that are logically derivable from other rules.

## Candidate Analysis

### Candidate 1: "Never SELECT * in production queries" (S7)
- **Potentially entailed by**: "select only the columns you need" in the same sentence
- **Verdict**: NOT REDUNDANT. The prohibition is grep-scannable for CI enforcement (iteration 31-32 gates). The positive instruction guides implementation. Different purposes: one is a gate, the other is guidance.

### Candidate 2: "Test behavior not implementation" (S5)
- **Potentially entailed by**: "Mock at boundaries only" + "If you refactor internals and tests break the tests were wrong"
- **Verdict**: NOT ENTAILED. The principle is broader — it covers method-level testing decisions beyond mock placement. The examples are consequences of the principle, not equivalent to it.

### Candidate 3: "Never store local times in the database" (S14)
- **Potentially entailed by**: "Store all timestamps in UTC"
- **Verdict**: COMPLEMENTARY, NOT REDUNDANT. Positive instruction + negative instruction pattern. AI agent might generate `NOW()` without timezone awareness; the negative instruction catches the antipattern specifically.

### Candidate 4: "Linear history preferred" (S1)
- **Potentially entailed by**: "rebase feature branches onto target before merge"
- **Verdict**: NOT REDUNDANT. The principle statement explains *why* rebase is done. Removing it makes the rebase instruction procedural without rationale.

### Candidate 5: "Never read process.env in random places" (S4)
- **Potentially entailed by**: "config/ loaded once at startup" + "Never import config inside business logic"
- **Verdict**: CLOSE but NOT ENTAILED. The `process.env` prohibition catches direct env access that bypasses the config system entirely. The config rules only prevent config *module* imports in wrong places. Different attack vectors.

### Candidate 6: "Circular imports are architecture bugs" (S2)
- **Potentially entailed by**: Dependency direction rules (handlers→services→core→adapters)
- **Verdict**: NOT ENTAILED. Circular imports can occur *within* a layer (service A ↔ service B). The dependency direction rules only prevent cross-layer violations.

## Meta-Assessment

All 6 candidates rejected. The remaining rules serve independent purposes:
- Gate vs guidance (Candidate 1)
- General principle vs specific consequence (Candidate 2)
- Positive vs negative instruction (Candidate 3)
- Rationale vs procedure (Candidate 4)
- Different attack vectors (Candidate 5)
- Different violation scopes (Candidate 6)

## Lens Verdict: REJECTED

This lens is subsumed by the compression passes (iterations 23-37) which already evaluated rule-level redundancy at multiple granularities. The compression passes achieved diminishing returns (380 → 325 → 115 → 57 → 27 words), reaching the floor at iteration 37. Remaining apparent redundancies follow the intentional "principle + prohibition + positive instruction" teaching pattern.

Furthermore, the document's design philosophy (documented across 140+ low-severity observations) explicitly values redundancy when removal would require multi-step logical derivation by the reader. The primary consumer (AI agent) benefits from explicit rules over implicit entailment.

## Status
- 16th consecutive zero-edit iteration
- 43 total lens applications (30 unique + 13 verification/rejection passes)
- Protocol remains at terminal state
