# Iteration 74: Negative Space Coverage Audit

## Lens
Do any "wrong" examples in the document describe patterns that are sometimes correct, potentially misleading a reader who follows the document literally?

## Method
Extracted all 19 "wrong is" / "Wrong is" anti-pattern labels across the document. For each, assessed whether the label is always wrong or context-dependent.

## Findings

### Classification
- **4 genuinely always wrong** (SQL injection, shell injection, logging credentials, vague review feedback)
- **1 nearly always wrong** (dead commented-out code)
- **14 "wrong by default but sometimes right"** (direct imports, nested conditionals, optional fields, what-comments, direct library imports, process.env reads, innerHTML, sequential awaits, console.log, bug+refactor, callsite null checks, optional userId, catch-and-continue, TODO comments)

### Falsification of the 14 Context-Dependent Items

Every one of the 14 items is already scoped by qualifying phrases in the document:

1. **"Wrong is describing what code does BECAUSE THE CODE ALREADY SAYS THAT"** — scopes to redundant restatement, not API contract documentation. JSDoc/docstrings describe contracts, not restate code.

2. **"Wrong is sequential awaits WHEN OPERATIONS ARE INDEPENDENT"** — rate-limited shared APIs create a dependency. The qualifier handles this.

3. **"wrong is catching processOrder and logging 'order failed continuing'"** — the criminal label is on the *specific pattern* of logging without context and continuing silently. Section 15 explicitly endorses dead letter queues and Section 3's error handling requires context. Batch processing with proper error handling is not the pattern labeled "wrong."

4. **"wrong is element.innerHTML = userInput"** — the operand is raw `userInput`, not sanitized content. Sanitized HTML is no longer raw user input.

5. **"Wrong is import { userRepo } from '../adapters/db' at module level inside the service"** — scoped to services specifically. CLIs, scripts, and serverless functions are not services in the architecture.

6. **"wrong is reading process.env.SENDGRID_KEY inside a sendEmail function"** — scoped to business logic functions, not to all code. Config at startup is the rule for services.

7. **"Wrong is console.log with string concatenation"** — Section 12 explicitly has a Temporary Debug Logging Protocol for investigation. The "wrong" is production code, not all contexts.

8. **"wrong is fixing the bug AND refactoring"** — iteration 50 already added an exception for when the refactor reveals the bug. Section 20 step 3 addresses the refactor-reveals-bug case.

9. **"wrong is adding null check at every callsite...which treats symptoms"** — the qualifier "which treats symptoms" scopes this. Phase 4 Commit 3 explicitly endorses defensive checks found in blast radius search.

10. **"wrong is optional userId that should always be there"** — the qualifier "should always be there" scopes this. Pre-auth contexts genuinely don't always have a userId.

11. **"wrong is nested if statements...with actual logic buried 3 levels deep"** — the depth is the issue, not all nesting. Guard clauses replace depth, not structured pattern matching.

12. **"wrong is a single Order interface...that allows impossible states"** — scoped to type design. Database rows needing flat representation at the adapter layer are the adapter's concern, not core's.

13. **Direct library imports (dayjs across 47 files)** — the 47-file qualifier implies scale. Wrapping a library used in 3 files is not the same situation.

14. **TODO without fixing** — Section 11 permits TODOs with ticket references. The "wrong" is TODO without action, not TODO as a pattern.

### Verdict
**Zero HIGH findings.** All "wrong" labels are either genuinely absolute (security patterns) or already scoped by qualifying phrases that prevent literal misapplication. The document's qualifiers (because/when/that/which clauses) correctly narrow each anti-pattern to its genuinely-wrong domain.

### Comparison to Prior Lenses
This lens is novel — no prior lens examined whether the document's negative examples (anti-patterns) could be false negatives. Related but distinct from:
- Adversarial compliance (iteration 60): tested whether rules could be gamed by letter-over-spirit compliance
- Scope boundaries (iteration 55): tested whether absolute rules were over-broad
- Misapplication recovery (iteration 62): tested whether honest mistakes produce feedback

This lens tests whether the *examples themselves* are misleading, which is an orthogonal concern.

### Low-Severity Observations
None promoted to editing threshold. The qualifying phrases are sufficient.
