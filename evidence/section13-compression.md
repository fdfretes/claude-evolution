# Section 13 API Design Standards Compression — Evidence

## Analysis Date: 2026-02-17

## Redundancies Identified

### 1. Status Code Tutorial Content (~35 words recoverable)
**Problem**: Full status code list includes obvious codes (200, 204, 400, 404, 500) alongside non-obvious distinctions (401 vs 403, 409, 422, 429). A developer reading this standards document already knows what 200 and 404 mean. The non-obvious distinctions are the actual value: they prevent common mistakes.

**Additional duplication**: "201 created with Location header" appears in both the HTTP methods section (POST for create returning 201 with Location header) and the status code list. Redundant — the POST mapping already specifies the status code and header.

**Compression**: Keep "Status codes are not suggestions" (the principle). Replace full list with "Use standard codes correctly. Non-obvious distinctions:" followed by only 401 vs 403, 409, 422, 429.

**What's preserved**: The five non-obvious distinctions that prevent actual mistakes. All standard codes (200, 201, 204, etc.) are universally known and don't need definition.

### 2. Idempotency Implementation Detail (~22 words recoverable)
**Problem**: "Implementation: hash the idempotency key store in Redis or database with TTL and check before processing" is a how-to sentence. The preceding content already states the standard: "Store the key and response for 24 hours. If the same key is sent again return the stored response without re-executing."

**Compression**: Remove the implementation sentence entirely. The standard (store key+response, check before processing) is already stated.

**Additional compression**: "duplicate orders duplicate payments and duplicate side effects" → "duplicate side effects" — orders and payments are instances of side effects. The precise term subsumes the examples.

### 3. REST URL Anti-Examples (KEPT — not redundant)
**Analyzed**: Whether "/api/users/:id/orders not /api/getUserOrders" duplicates "/api/users not /api/getUsers".
**Finding**: They demonstrate different principles. First shows nouns-not-verbs. Second shows resource nesting. Each anti-example is unique.
**Decision**: Keep both.

### 4. Response Envelope vs Section 3 Error Format (KEPT — not redundant)
**Analyzed**: Whether `{ error: { code, message, details? } }` in Section 13 duplicates the AppError class in Section 3.
**Finding**: Section 3 defines the internal error class shape. Section 13 defines the API response contract. They serve different purposes (internal vs external). Both are needed.
**Decision**: Keep both.

## Falsification Results

| Compression | Risk | Assessment |
|---|---|---|
| Remove obvious status codes | Loses "complete reference" value | Safe — this is a standards doc, not HTTP reference. Non-obvious distinctions are the value. |
| Remove idempotency implementation | Devs might implement incorrectly | Safe — the what-to-do is already stated. Redis/DB is technology-specific. |
| Compress "prevents" list | Less concrete/memorable | Safe but marginal — "side effects" is precise and context is clear. |
| Remove second REST anti-example | Loses nesting demonstration | NOT safe — demonstrates a different principle (nesting vs nouns). KEPT. |

## Applied Changes
- Edit 1: Status code list compressed to non-obvious distinctions only (~35 words saved)
- Edit 2: Idempotency implementation sentence removed + "prevents" list compressed (~22 words saved)
- Total: ~57 words saved

## What Was NOT Compressed
- REST conventions and anti-examples (each demonstrates a unique principle)
- Response envelope (external API contract, not a duplicate of internal error class)
- Pagination contract (compact already)
- Versioning rules (each rule is actionable and distinct)
- Deprecation lifecycle (added iteration 33, already tight)
- Rate limiting (compact already)
