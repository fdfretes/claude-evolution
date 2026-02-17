# Cross-Format Consistency Audit

## Lens: Cross-Format Consistency (25th lens)
Do the structured output formats prescribed across sections use consistent naming conventions, field naming, and serialization rules?

## Formats Audited
1. Error response (Section 3 global error handler + Section 13 API envelope)
2. Log entry (Section 8 structured logging examples)
3. Health check response (Section 10)
4. API pagination envelope (Section 13)
5. WebSocket message (Section 24)
6. MQTT message schema (Section 23)

## Findings

### FINDING 1: No JSON key naming convention; mixed camelCase/snake_case in same example (MEDIUM)
- Section 8 log example mixes `userId` (camelCase) with `duration_ms` (snake_case) in the same object
- Section 3 naming conventions cover variables, functions, booleans, constants, collections, classes, files — but not JSON keys
- Document's own examples overwhelmingly use camelCase for JSON keys: `userId`, `orderId`, `statusCode`, `totalPages`, `createdAt`
- Section 23 (MQTT/IoT) uses snake_case: `device_id`, `message_type` — consistent with hardware ecosystem convention
- Gap is real: a developer writing a new log schema or API response has contradictory examples

**Action**: Add JSON key convention to Section 3 naming rules. Fix Section 8 mixed example.

### FINDING 2: MQTT vs WebSocket schema structural differences (LOW)
- Different protocols, different purposes, different field names — defensible divergence
- `message_type` (MQTT) vs `type` (WebSocket) maps to ecosystem conventions
**Action**: None. Correct by design.

### FINDING 3: ISO 8601 timestamp format only explicit for WebSocket (LOW)
- S24 says "ISO 8601 UTC"; S23 says "timestamp in UTC"; S8 says "timestamp" without format
- UTC requirement is universal but wire format not specified everywhere
**Action**: None. Below editing threshold — ISO 8601 is implied by the existing UTC mandate, the gotcha example in Section 3, and the `timestamptz` rule in Section 14.

### FINDING 4: Health check envelope differs from API envelope (LOW)
- Health check uses `{ status, checks }` not `{ data: ... }`
**Action**: None. Correct by design — health checks are infrastructure endpoints, not API endpoints.

### FINDING 5-7: ID naming, error structure, status semantics (LOW/NONE)
**Action**: None. All either resolved by Finding 1 or non-issues.

## Falsification

1. **IoT boundary**: Proposed rule explicitly carves out IoT/hardware protocol boundaries — MQTT's `device_id` stays as-is
2. **Variable naming conflict**: JSON keys face external consumers; source variables are internal. Different conventions for different audiences is valid. Document already does this (PascalCase for classes, kebab-case for files, camelCase for existing JSON examples)
3. **`duration_ms` → `durationMs`**: Follows same pattern as `timeoutMs`, `delayMs`. Unit suffix is preserved. Slightly less visually obvious but consistent with the declared convention
4. **Ecosystem assumption**: Document already contains JS/TS-specific patterns throughout. The camelCase choice codifies existing de facto practice from examples
5. **Real failure mode**: Mixed-convention keys in a single log entry would produce literally inconsistent JSON in production. A developer copying the Section 8 example verbatim generates inconsistent keys

## Edits Applied
1. Section 3: Added JSON key naming convention after file naming rule (~25 words)
2. Section 8: Fixed `duration_ms` to `durationMs` in log example (~1 word change)
