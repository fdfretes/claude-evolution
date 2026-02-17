# Rule Verifiability Audit (Iteration 54)

## Lens: Rule Verifiability
Can each absolute rule ("NEVER", "ALWAYS", "no exceptions") be mechanically verified? Distinct from enforcement audit (iterations 31-32) which checked if rules HAVE CI gates. This lens checks if rules are VERIFIABLE IN PRINCIPLE — whether a tool, linter, or systematic code review could confirm compliance, or whether the rule is inherently heuristic and therefore unfalsifiable as an absolute.

## Classification
- **Mechanically Verifiable (MV)**: A tool can check this (linter, grep, type checker, CI gate)
- **Review Verifiable (RV)**: A human/AI code reviewer can systematically verify this
- **Heuristic (H)**: Requires judgment; cannot be systematically verified as yes/no
- **CONCERN**: Rules stated as absolutes but are actually heuristic

## Audit of Absolute Rules by Section

### Section 1 (Git)
- "every commit MUST compile pass lint pass tests" — MV (CI)
- "NEVER mix logic+formatting in same commit" — RV (diff review)
- "Pre-Commit Protocol executed every time with no exceptions" — RV (process discipline)
- No concerns.

### Section 2 (Architecture)
- "core/ zero imports from adapters handlers external packages" — MV (import linter, CI gate in S21)
- "Max 15-20 lines per handler" — MV (line counter)
- "Never import config inside business logic" — MV (import linter)
- "services receive adapters via constructor or factory parameters never via direct import" — RV (review diffable pattern)
- No concerns.

### Section 3 (Code Standards)
- "Never name anything Helper Manager Handler without specificity" — **H** — "without specificity" is subjective. What makes "PaymentHandler" specific enough vs "Handler"? Convention: if the class name includes the domain (Payment, User, Order), the suffix is acceptable. This is already implicitly clear from the example (PaymentProcessor yes, ProcessManager no).
- "Max 3 parameters" — MV (linter)
- "No positional boolean parameters" — MV (linter detectable)
- "never nest beyond 3 levels" — MV (linter, complexity checker)
- "Max 30 lines per function" — MV (line counter)
- "NEVER swallow errors" — MV (linter rule for empty catch blocks); partial (can't catch `catch(e) { log(e) }` — the "negligent" case is harder)
- "No any" — MV (TypeScript strict mode + linter)
- No actionable concerns. The "specificity" judgment call is appropriate — can't define an algorithm for "specific enough."

### Section 4 (Dependencies)
- "can I write this in under 50 lines?" — **H** — requires estimation, but this is by design (it's a decision framework, not an absolute prohibition)
- No concerns (framed as decision questions, not absolutes).

### Section 5 (Testing)
- "Every bug fix ships with a regression test — non-negotiable" — RV (reviewer checks PR for test)
- "One logical assertion per test" — **H** — "logical" is subjective. Two assertEqual checks verifying different aspects of the same result could be one or two "logical assertions."
- **FINDING**: "One logical assertion per test" is stated as a rule but is actually a heuristic. However, it uses the word "logical" which inherently signals judgment. This is correctly self-scoping. No fix needed.
- "Flaky test equals P1 bug" — RV (CI can detect flaky tests via re-run)
- No actionable concerns.

### Section 6 (Security)
- "SQL is ALWAYS parameterized" — MV (CI gate per S21: injection pattern scanning)
- "Shell commands NEVER interpolate user input" — MV (CI gate per S21)
- "HTML ALWAYS escapes" — MV (CI gate per S21)
- "Never serialize domain objects directly to API responses" — RV (review checks for response mapping functions)
- "Never log secrets" — Partial MV (grep can detect common patterns); full verification requires judgment
- No actionable concerns.

### Section 7 (Performance)
- "Never SELECT * in production queries" — MV (grep/linter)
- "every external call has an explicit timeout" — **RV** — reviewable but hard to automate. A missing timeout is a silent default, not a present pattern.
- No actionable concerns. Timeout rule is appropriately absolute — the risk of infinite hangs justifies the review burden.

### Section 8 (Logging)
- "never log PII" — Partial MV (grep for common PII field names); full verification requires judgment about what constitutes PII
- "Never log credentials tokens or secrets period" — MV (grep patterns)
- No actionable concerns.

### Section 9 (Workflow)
- "Never generate calls to functions methods or imports from memory alone" — **H for AI agent** — the agent can't always distinguish "from memory" vs "from reading." However, the ACTIONABLE version is clear: "read the actual definition or type signature" which IS verifiable (did the agent read the file before calling the function?).
- No actionable concerns. The rule's action is verifiable even if the mental state isn't.

### Section 10 (Deployment)
- "Never update all devices simultaneously" (OTA, in S23 actually) — RV (deployment config review)
- "Never reuse a flag name" — MV (grep/search)
- No concerns.

### Section 11 (Communication)
- "NEVER DO: commit or output secrets" — MV
- "NEVER DO: use any types without justification" — MV (TypeScript linter + comment presence)
- All items verifiable. No concerns.

### Section 12 (Debugging)
- "NEVER apply a speculative fix to a bug you cannot reproduce" — **H** — "speculative" and "cannot reproduce" are judgment calls. However, this is philosophy/principle, not a mechanical rule. Appropriately stated as a directive, not a CI gate.
- No actionable concerns.

### Section 13 (API)
- "Never return raw arrays at top level" — MV (response type check)
- "Never remove fields without version bump" — RV (diff review between versions)
- No concerns.

### Section 14 (Database)
- "Never modify a migration that has been applied" — RV (migration file timestamps/checksums)
- "Never store local times" — RV (schema review for timestamptz vs timestamp)
- "Never rename a column directly in production" — RV (migration review)
- "always use CREATE INDEX CONCURRENTLY" — MV (migration file grep)
- No concerns.

### Section 15 (Resilience)
- "never retry immediately and never retry forever" — RV (code review for retry logic)
- "Never retry on 4xx except 429" — RV (code review)
- "Never drop messages silently" — RV (code review for error/DLQ handling)
- No concerns.

### Section 16 (Caching)
- "Never cache errors" — RV (code review)
- No concerns.

### Section 17 (Concurrency)
- "Never hold a database lock while making an external HTTP call" — **RV** — reviewable but requires understanding the full code path inside a lock, not just the immediate block. This is a cross-function concern.
- No actionable concerns. The rule is correct and important; the verification difficulty is inherent to the problem domain.

### Section 22 (Secrets)
- "never rotate manually" — Process rule, not code-verifiable
- No concerns (operational directive, appropriately stated).

## Summary

### All absolute rules assessed: ~45+
### Classification breakdown:
- Mechanically Verifiable: ~25 (linter, CI, grep)
- Review Verifiable: ~15 (code review, diff analysis)
- Heuristic (appropriately scoped): ~5 (use judgment words like "logical", "specific", "speculative")
- **Concerns: 0**

### Key Finding
Every absolute rule in the document is either:
1. Mechanically verifiable (and connected to CI gates per iterations 31-32), or
2. Review-verifiable (and part of S25 code review checklist items), or
3. Appropriately self-scoped as heuristic using language that signals judgment ("logical assertion", "without specificity", "speculative fix")

The document does NOT have any false absolutes — rules stated as mechanical/enforceable that are actually heuristic. The escape hatch pattern from iteration 40 (any/unknown) and the scope qualifier from iteration 26 (max 3 params) were the cases where this was a problem, and both have been fixed.

### Verdict: No edits needed. The document's absolute rules are well-calibrated to their verifiability.
