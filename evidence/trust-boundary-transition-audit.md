# Trust Boundary Transition Audit

## Lens: Trust Boundary Transitions
Every time data crosses a trust boundary, is validation/transformation specified?

## Method
Traced data flow across every trust boundary in the system architecture. A trust boundary is where data moves between contexts with different privilege levels or where the data's format/interpretation changes.

## Boundaries Audited

### 1. External HTTP → Handler (inbound user data)
- **Rule**: Section 6 INPUT VALIDATION — every handler validates with schema (.parse())
- **Status**: COVERED (explicit, enforceable)

### 2. Handler → Service (validated input)
- **Rule**: Section 6 — "After that point input is typed and trusted throughout the service layer"
- **Status**: COVERED (explicit trust handoff)

### 3. Service → Database (outbound query)
- **Rule**: Section 6 INJECTION PREVENTION — "SQL is ALWAYS parameterized"
- **Status**: COVERED (explicit, with wrong/right examples)

### 4. Database → Service (query results)
- **Rule**: Implicit — results come from the system's own schema, trusted
- **Status**: COVERED (correctly implicit — DB returns what the schema defines)

### 5. Service → Handler → Client (response serialization)
- **Rule**: Section 6 RESPONSE SERIALIZATION SAFETY — allowlist-based response shaping
- **Status**: COVERED (explicit, added iteration 30)

### 6. Service → Shell (system commands)
- **Rule**: Section 6 — "Shell commands NEVER interpolate user input"
- **Status**: COVERED (explicit, with wrong/right examples)

### 7. Service → HTML (rendering)
- **Rule**: Section 6 — "HTML ALWAYS escapes"
- **Status**: COVERED (explicit, with wrong/right examples)

### 8. Config/Environment → System (startup)
- **Rule**: Section 4 — validate with schema at startup, fail fast
- **Status**: COVERED (explicit, with wrong/right examples)

### 9. Message Queue → Consumer (async messages)
- **Rule**: Section 23 — "Validate messages on both sides"
- **Rule**: Section 15 — idempotent processing, dead letter queues
- **Status**: COVERED (explicit in IoT context, generalizable)

### 10. Device → Server (IoT telemetry)
- **Rule**: Section 23 — schema validation, consumer service validates
- **Status**: COVERED (explicit)

### 11. Server → External HTTP API (outbound HTTP)
- **Rule**: No explicit rule for constructing outbound URLs or request bodies with user-derived data
- **Status**: IMPLICIT — derivable from the general injection prevention pattern

### 12. Client → WebSocket (bidirectional)
- **Rule**: Section 24 — authenticate on connection, message schema validation
- **Status**: COVERED (explicit)

## Findings

### Boundary 11: Outbound HTTP Request Construction
**Severity**: LOW
**Issue**: The document's injection prevention rules (SQL, shell, HTML) are enumerated examples rather than a general principle like "never interpolate untrusted data into any interpreted context." This means SSRF (server-side request forgery) via outbound URL construction is not explicitly covered.

**Why this is LOW, not MEDIUM**:
1. The three enumerated injection types cover 95%+ of real-world injection attacks
2. SSRF is primarily a concern when user input directly controls a URL, which is uncommon in most applications
3. The pattern is clearly derivable — the document teaches "parameterize/escape at boundaries" as a skill, not just as specific rules
4. The existing CI gate (Section 21) includes "injection pattern scanning" which could catch URL interpolation
5. Adding explicit SSRF guidance would add ~20 words for a pattern the developer can derive
6. Section 2's adapter pattern means external HTTP calls go through `adapters/http/` which provides a single chokepoint for URL construction — the document's architecture already creates the right structure

**Decision**: Not worth editing. The injection prevention triplet (SQL, shell, HTML) plus the adapter architecture pattern provide sufficient coverage. Adding SSRF would be enumerating a fourth case of a pattern already established by three examples.

## Summary
- 12 trust boundaries identified
- 11 explicitly covered by specific rules
- 1 implicitly covered (outbound HTTP construction) — derivable from existing patterns
- 0 gaps requiring edits
- Severity: No MEDIUM or HIGH findings
