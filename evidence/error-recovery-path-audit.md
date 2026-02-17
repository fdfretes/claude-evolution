# Error Recovery Path Completeness Audit

## Lens Definition
When the document prescribes a multi-step procedure and a step can fail, does the document provide guidance on what to do next? This is distinct from:
- **Failure mode asymmetry** (iteration 49): checks protective density proportional to severity
- **Constraint stacking composability** (iteration 50): checks rules compose cleanly under simultaneous application
- **Prerequisite chain completeness** (iteration 48): checks every instruction has an actionable implementation path

This lens asks: **within single procedures, are there unstated failure-branch recovery paths?**

## Procedures Audited

### 1. Pre-Commit Protocol (S1), Steps 1-6
- **Step 3 failure (secret detected)**: "stop unstage and remediate" — explicit recovery. ✅
- **Step 4 failure (contamination found)**: "evaluating if matches are intentional or leftover" — implicit branch (remove if leftover, keep if intentional). ✅
- **Step 5 failure (not atomic)**: Implicit: split the commit. Derivable from Law 1 + "If you need the word 'and' it is two commits." ✅

### 2. Graceful Shutdown (S3), Steps 1-4
- **Step 2 failure (drain timeout exceeds 30s)**: Timeout specified (30s), implicit force-exit after. ✅
- No step can fail without recovery path.

### 3. Before Writing Code (S9), Steps 1-5
- **Step 2 reveals existing solution**: "you must not reinvent what exists" provides the recovery path (use it). But the procedure then says "3 DESIGN the interface" with no explicit "if not found" gate.
- **Assessment**: LOW severity. The phrase "must not reinvent" is the gate. An experienced reader stops. An AI agent following literally might continue to step 3. But the "verify before generating" rule in the same step partially mitigates this.
- **Edit candidate?** ~8 words ("If no existing solution fits, then:"). Below threshold — the behavior is derivable.

### 4. Debugging Phase 4 (S12) — Three Commits
- **Phase 3 finds no similar patterns**: "Three commits minimum" but Commit 3 is for similar patterns. If none found, only 2 commits needed.
- **Assessment**: LOW severity. "Minimum" combined with "similar patterns found in Phase 3 blast radius search" makes it conditional. An AI agent might create an empty Commit 3. Minor.
- **Edit candidate?** ~4 words ("if similar patterns found"). Below threshold — derivable from context.

### 5. Zero-Downtime Migration (S14), Phases 1-4
- **Phase 2 backfill fails midway**: No guidance on partial backfill recovery.
- **Assessment**: LOW severity. This is inherently project-specific (depends on migration tooling). Already noted in frontier.md low-severity observations.

### 6. Emergency Hotfix Protocol (S12), Steps 1-6
- **Step 4 (tests) fails**: No explicit branch. Implicit: fix the test failure or reconsider the approach.
- **Assessment**: LOW severity. Under emergency pressure, the instruction "deploy through the pipeline" in Step 5 implicitly requires Step 4 to pass. If tests fail, you iterate.

### 7. Section 4 Config Validation
- **safeParse fails**: "console.error the flattened errors and process.exit(1)" — explicit crash-at-startup recovery. ✅

### 8. Section 15 Retry with Exponential Backoff
- **All retries exhausted**: No explicit "what next" guidance.
- **Assessment**: LOW severity. The caller receives the error and handles it per Section 3 error handling rules. The error propagates up the stack to the handler's catch boundary. Derivable from the overall error handling architecture.

### 9. JWT Key Rotation Overlap (S22)
- **Overlap period unspecified**: "overlap period where both old and new key are valid" but no duration.
- **Assessment**: LOW severity. ~15 words to specify "overlap period equals at least the maximum token lifetime." Operationally important but narrow. Below the document's editing threshold established by iterations 37+.

## Summary

| Procedure | Recovery Gap | Severity | Edit Worthy? |
|-----------|-------------|----------|-------------|
| S9 Steps 2→3 | No explicit "if found, stop" gate | LOW | No (derivable from "must not reinvent") |
| S12 Phase 4 | "Three commits minimum" when Commit 3 may not apply | LOW | No (derivable from conditional context) |
| S14 Phases 1-4 | Partial backfill recovery unspecified | LOW | No (project-specific) |
| S22 JWT overlap | Duration unspecified | LOW | No (narrow operational detail) |
| S15 retry exhaustion | No "what happens after all retries fail" | LOW | No (derivable from error handling architecture) |

## Conclusion

**0 findings above editing threshold.** All recovery paths are either explicitly stated or derivable from adjacent rules. The document's error handling architecture (S3: handlers catch, services throw, core returns typed errors) serves as a universal implicit recovery mechanism — when any step fails, the error propagates to the catch boundary.

This is the 24th distinct lens applied to the document. It confirms the document's maturity: even analyzing failure branches within procedures yields no actionable gaps.
