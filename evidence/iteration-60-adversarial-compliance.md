# Iteration 60: Adversarial Compliance Testing

## Lens Description
Can a malicious or lazy practitioner satisfy the letter of the rules while violating their spirit? This is distinct from iteration 59's cooperative scenario simulation, which tested what happens when a practitioner follows instructions in good faith. This lens tests the document's resistance to gaming.

## Why This Lens Is Novel
- Iteration 59 tested cooperative compliance (following instructions produces correct results)
- This lens tests adversarial compliance (trying to game rules produces blocking counterexamples)
- A mature standards document should resist rules-lawyering through intent clauses, not just mechanical constraints

## Adversarial Scenarios Tested

### 1. Function Length Gaming
**Attack**: Extract trivially small 1-line helpers to get a 100-line function under 30 lines while making it harder to read.
**Defense**: Preamble "clarity over cleverness" + S20 "extract function when a block of code has a single responsibility and a natural name." Trivial extractions without natural names violate naming rules.
**Verdict**: BLOCKED by intent clause.

### 2. Test Assertion Combining
**Attack**: Write `expect(a && b && c).toBe(true)` to satisfy "one logical assertion per test."
**Defense**: Rule says "a failing test immediately tells you what broke" — combined assertion fails this intent test.
**Verdict**: BLOCKED by intent clause.

### 3. Trivial Regression Tests
**Attack**: Write `assert(true)` to satisfy "every bug fix ships with a regression test."
**Defense**: S5 "test behavior not implementation" + Phase 1 "write the reproduction FIRST as a failing test that MUST fail before you touch any source code" — a test that never fails cannot satisfy the "currently fails" requirement.
**Verdict**: BLOCKED by Phase 1 failing-test requirement.

### 4. Permissive Validation
**Attack**: Use `z.any()` to technically "validate at boundaries."
**Defense**: "No any" rule + S6 concrete examples (email, name, password) set strictness expectations. `.strict()` requirement rejects unknown fields.
**Verdict**: BLOCKED by cross-rule interaction.

### 5. Enumerate All Columns
**Attack**: `SELECT col1, col2, ..., col50` to satisfy "Never SELECT *" while selecting everything.
**Defense**: Rule says "select only the columns you need" — the "you need" intent clause prevents over-selection.
**Verdict**: BLOCKED by intent clause.

### 6. Giant Options Object
**Attack**: Create single options object with 15 required fields to dodge "max 3 parameters."
**Defense**: This is actually the intended pattern for genuinely complex operations. Named fields provide readability. If 15 fields aren't truly needed, "max 30 lines per function" limits the function's scope naturally.
**Verdict**: NOT AN ATTACK — correctly permitted.

### 7. Micro-Commits
**Attack**: Commit 1-character changes to technically satisfy "atomic commits."
**Defense**: Law 3 "structure commits for the reviewer" + Newspaper Test "does each line represent exactly one logical change?" — incomplete changes fail both.
**Verdict**: BLOCKED by reviewer-centric intent.

### 8. Security Scan Variable Naming Evasion
**Attack**: Name an API key variable `authCode` to evade the grep pattern `secret|key|token|password|api_key|credential|private_key`.
**Defense**: S3 naming rules require constants to describe MEANING (`API_KEY`, `AUTH_TOKEN`). A credential named `authCode` violates naming rules. The variable name `key` is also broadly caught by the pattern.
**Verdict**: BLOCKED by cross-rule interaction (S3 naming → S1 security scan).

### 9. Numeric Boolean Substitution
**Attack**: Use `0/1` instead of `boolean` to dodge "no positional boolean parameters."
**Defense**: S3 "variables describe what it IS" — a number representing a boolean flag violates naming/typing conventions.
**Verdict**: BLOCKED by type safety rules.

### 10. Flag Name Near-Reuse
**Attack**: Create `enable-dark-mode-v2` after removing `enable-dark-mode`.
**Defense**: This IS different name — correctly permitted. The rule prevents accidental reuse of exact names that might have stale cached values.
**Verdict**: NOT AN ATTACK — correctly permitted.

## Key Finding

The document resists adversarial compliance through a consistent architectural pattern:

**Every mechanical constraint is paired with an intent clause.**

- "Max 30 lines" + "extract sub-functions with descriptive names that serve as documentation"
- "Never SELECT *" + "select only the columns you need"
- "One assertion per test" + "a failing test immediately tells you what broke"
- "Atomic commits" + "structure for the reviewer" + Newspaper Test

The intent clauses prevent letter-vs-spirit gaming because they describe the OUTCOME the rule serves, not just the mechanical check. An adversarial consumer can satisfy the mechanical constraint but cannot satisfy the intent clause simultaneously with their gaming strategy.

## Conclusion

Zero gaps found. The document's defense against adversarial compliance is structural: the mechanical-constraint + intent-clause pairing pattern appears consistently across all tested rules. No edits needed.

## Cross-Reference to Previous Lenses
- Rule verifiability (iteration 54): classified rules as mechanical vs heuristic — this lens tests whether mechanical rules can be gamed when intent clauses are heuristic
- End-to-end scenario simulation (iteration 59): cooperative compliance — this lens complements with adversarial compliance
- Scope boundaries (iteration 55): tested whether absolute rules over-apply — this lens tests whether they under-apply through gaming
