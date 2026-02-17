# Iteration 67: Imperative Completeness Audit

## Lens Description
Audit every imperative directive ("never do X", "always do Y", "use Z") for whether it has sufficient operands: WHAT to do, WHERE to do it, WHEN to do it. A novel lens not previously applied — prior lenses checked contradictions, gaps, compression, cross-references, numeric constraints, scope boundaries, etc., but not whether each "verb" has all its necessary "objects."

## Findings (7 total: 1 HIGH-assessed, 6 MEDIUM)

### Finding 1: "--skip without understanding" (S1 Branching)
- **Severity:** MEDIUM
- **Issue:** "resolve conflicts properly never using --skip without understanding" — WHEN is --skip acceptable? What constitutes "understanding"?
- **Disposition:** Judgment-dependent by design. Same pattern as "merge conflict resolution guidance is minimal" (LOW-severity note from iteration 64). Specifying a --skip checklist would be overly prescriptive for a rare edge case.

### Finding 2: Resource cleanup on firmware/IoT (S3 → S23)
- **Severity:** MEDIUM
- **Issue:** "Every acquired resource must be released in a finally block" — doesn't map to C/Arduino embedded patterns (RAII, GPIO cleanup in shutdown handlers).
- **Disposition:** Section 23's firmware/server separation means firmware follows platform idioms. Adding C-specific cleanup patterns violates language-agnostic principle. Same rejection rationale as pre-seeded "Language-Specific Subsections" graveyard item.

### Finding 3: "Production queries" scope (S7)
- **Severity:** MEDIUM
- **Issue:** "Never SELECT * in production queries" — does "production query" include migration/backfill scripts?
- **Disposition:** Intent clearly derivable from context — "all queries in source code" is the obvious reading. Migration backfill scripts that transform data may legitimately need `SELECT *`. Risk is LOW.

### Finding 4: OTA rollback mechanism underspecified (S23)
- **Severity:** MEDIUM
- **Issue:** "Provide rollback mechanism" is the least-specified directive in the document (no WHAT/HOW/WHEN).
- **Disposition:** OTA rollback implementation (A/B partitioning, bootloader selection, health checks) is deeply hardware-specific. Specifying would add 50+ words of ESP32-specific guidance, violating technology-agnostic principle. Parallel to existing approach where Section 23 provides architectural patterns, not implementation details.

### Finding 5: DLQ alert threshold missing (S15)
- **Severity:** MEDIUM
- **Issue:** "Monitor dead letter queue size and alert when it grows" — no threshold specified, unlike other alert directives in S18.
- **Disposition:** DLQ alert thresholds are workload-dependent. A specific number would be wrong for most workloads. Section 18 gives representative thresholds for common alerts but infrastructure-specific monitoring is intentionally left to operational judgment. Same pattern as "performance budget numbers will shift with hardware" (LOW-severity note, iteration 63).

### Finding 6: Pre-commit grep secret scanning gap (S1)
- **Severity:** Initially assessed HIGH, downgraded to MEDIUM
- **Issue:** The grep pattern doesn't catch modern token formats (AWS `AKIA...`, GitHub `ghp_...`) that lack keyword=value syntax.
- **Disposition:** Defense-in-depth is intentional: grep is the local heuristic, gitleaks/truffleHog (S21) is the CI comprehensive scanner. The "no exceptions" framing refers to running the protocol, not to the grep being omniscient. Same pattern as iteration 53 finding: "CI tooling for injection scanning and architecture verification is intentionally tool-agnostic."

### Finding 7: "Update documentation" artifact mapping (S9)
- **Severity:** MEDIUM
- **Issue:** "Update documentation if behavior changed" — which documentation artifact?
- **Disposition:** Intentionally broad because the specific artifact depends on what changed. API changes → API docs; config changes → .env.example; deployment changes → runbooks. Creating a mapping table would add ~80 words for marginal precision. Context makes the intent clear.

## Assessment

All 7 findings fall into established categories already identified as below editing threshold:
1. **Firmware/platform-specific guidance** (Findings 2, 4): Same rejection as language-specific graveyard items
2. **Judgment-dependent directives** (Findings 1, 3, 7): Intentionally heuristic, same as 14+ existing LOW-severity notes
3. **Workload-dependent thresholds** (Finding 5): Same as performance budget caveat
4. **Defense-in-depth layers** (Finding 6): grep + CI scanner is deliberate two-layer design

## Decision: REJECT all findings (no edits)

None meet improvement criteria:
- Would not make standards clearer without making them longer
- Don't catch failure modes the current version misses (defense-in-depth exists)
- Would add 50+ words collectively for edge cases
- Most are derivable from existing patterns and context

## Novel Lens Contribution
The imperative completeness lens identified the same terminal-state signature as the previous 12 iterations: findings exist at LOW/MEDIUM severity but all fall below the editing threshold due to being judgment-dependent, platform-specific, workload-dependent, or addressed by defense-in-depth. The document's imperative directives are operationally complete for their intended audience.
