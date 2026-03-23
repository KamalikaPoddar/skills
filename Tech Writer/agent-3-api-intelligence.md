# Agent 3 — API Intelligence

The synthesis brain. Merges ticket data + codebase data + existing spec.
Declares one of four modes before Agent 6 can generate any YAML.
Agent 6 cannot run without a Mode Declaration from this agent.

---

## Mode Selection Logic

```
Codebase Intelligence Pack present? (Agent 1B ran in Claude Code/Cursor)
│
├── YES, schema + enums + routes extracted?
│   ├── All fields present → MODE A (Full Generation)
│   └── Some fields missing → MODE A with targeted [VERIFY] flags
│
└── NO (web mode or files not found)
    │
    ├── Existing openapi.yaml covers this endpoint?
    │   ├── Endpoint exists, just updating → MODE B (Spec Enrichment)
    │   └── Endpoint new or substantially changed → MODE B with gaps
    │
    └── No existing spec
        ├── PR diff / code snippet provided? → MODE C (PR-Informed Stub)
        └── Ticket data only → MODE D (Skeleton Only)
```

---

## Mode Profiles

### MODE A — Full Generation
Sources: codebase files + ticket
Field names: directly from serializer/schema code (zero invention)
Types: from type annotations
Enums: from enum class / choices declaration
Examples: from test fixtures if found, otherwise constructed
YAML: complete, accurate, merge-ready

### MODE B — Spec Enrichment
Sources: existing openapi.yaml + ticket
What to do: find relevant path block → keep existing fields unchanged
→ add new fields from ticket (flag ambiguous names) → add/update descriptions
→ add x-changelog annotation → set x-breaking if applicable → update examples
Field names: authoritative from spec; new fields from ticket (flag if inferred)

### MODE C — PR-Informed Stub
Sources: PR description or diff snippet + ticket
Changed fields: HIGH confidence from diff
Unchanged context: MEDIUM from ticket + spec if available

### MODE D — Skeleton Only
Sources: ticket data alone
Every field name, type, enum value not explicitly stated in ticket:
→ marked `# [VERIFY WITH ENGINEER]`
Structure is useful scaffold for engineers to fill in.
Must NOT be published without engineer review.

---

## API Intelligence Report (one per API_CHANGE ticket)

```
╔════════════════════════════════════════════════╗
  API INTELLIGENCE REPORT
  Ticket: [PROJ-ID] — [Title]
  Endpoint: [METHOD] [/path]
  Mode: [A / B / C / D]
╠════════════════════════════════════════════════╣

SOURCE CONFIDENCE:
  Field names: [HIGH from serializer / MEDIUM from ticket / LOW inferred]
  Types:       [HIGH from annotations / MEDIUM / LOW]
  Enums:       [HIGH from enum class / MEDIUM from ticket / LOW]
  Examples:    [REAL from tests / CONSTRUCTED / PLACEHOLDER]

VALIDATED FACTS (use directly in YAML):
  ✓ amount → float, required, min:0.01 (transfers/serializers.py:14)
  ✓ currency → string, required, enum:[INR,USD,GBP] (enums/currency.py:8)
  ✓ status → enum:[pending,processing,settled,failed] (enums/status.py:3)

UNVERIFIED (flag in YAML):
  [VERIFY] recipientBankCode — in ticket AC but not found in serializer.
           Confirm: exact field name? required or optional?
  [VERIFY] errorCode — referenced in AC but no enum found.
           What are the valid error code values?

BREAKING CHANGE ASSESSMENT:
  Breaking: [Yes / No / Possibly]
  If yes: what breaks, who affected, migration steps

YAML SECTIONS TO GENERATE:
  ☑ New path: POST /api/v2/transfers/batch
  ☑ New schema: BatchTransferRequest
  ☑ New schema: BatchTransferResponse
  ☑ API Changelog entry
╚════════════════════════════════════════════════╝
```

---

## Detecting Breaking Changes from Code

```
BREAKING signals:
  Field renamed → migration file shows RENAME COLUMN, or serializer has source= pointing elsewhere
  Field type changed → model migration changes column type
  Field removed → present in previous spec/serializer, now absent
  Enum value removed → enum class has fewer values than previously documented
  Endpoint path changed → old route no longer in router file
  Auth added to previously public endpoint

NON-BREAKING (additive):
  New optional field in response
  New optional query parameter
  New endpoint added
  New enum value added (clients ignore unknown values)
```

---

## Fintech Intelligence Flags

For payment/financial endpoints, also check:

```
☑ IDEMPOTENCY: Idempotency-Key header middleware present?
  If absent → flag: [CONSIDER: Idempotency header needed for safe retries?]

☑ CURRENCY UNITS: Amounts as integers (paise/cents) or floats?
  Look for: amount * 100, DecimalField, integer column in migration
  Note in YAML description: "Amount in [currency] [base units or decimal]"

☑ RATE LIMITING: throttle_classes / @ratelimit / rate_limit middleware present?
  If yes → document 429 + Retry-After header in YAML

☑ WEBHOOKS: Outbound webhooks triggered by this endpoint?
  If yes → document webhook payload shape as separate schema block
