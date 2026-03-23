# Agent 1B — Codebase Reader

The primary accuracy path for AI-native PMs. Reads targeted source files
to extract exact field names, types, enum values, and examples.

---

## Two Execution Modes

### Claude Code / Cursor (Primary)

```bash
# Auto-locate relevant files
find . -name "*serializer*" -o -name "*schema*" -o -name "*dto*" 2>/dev/null | head -20
find . -name "*enum*" -o -name "*constant*" -o -name "*choices*" 2>/dev/null | head -20
find . -name "openapi.yaml" -o -name "swagger.yaml" -o -name "swagger.json" 2>/dev/null
find . -path "*/tests/*" -name "*.json" 2>/dev/null | head -10   # golden payloads
find . -path "*/migrations/*" | sort -r | head -5               # recent schema changes
```

Announce: "Running in Claude Code — reading codebase directly for Mode A accuracy."

### Claude.ai Web (Fallback)

Ask: *"Paste any of these (in value order):
1. Serializer/schema file for the changed resource
2. Route/controller file for the changed endpoint
3. Enum/constants file
4. Existing openapi.yaml
5. A test file with real request/response examples"*

---

## Framework File Targets + Extraction Rules

### Python — Django/DRF
- `serializers.py` → field names, required flags, read_only, choices
- `models.py` → TextChoices enums (source of truth for enum values)
- `views.py` → HTTP methods, permission_classes
- `urls.py` → exact paths

Enum pattern: `class TransferStatus(models.TextChoices): PENDING = 'pending', 'Pending'`

### Python — FastAPI
- `schemas.py` → Pydantic models (1:1 with OpenAPI schema)
- `routers/*.py` → route definitions, type hints
- `enums.py` → Enum classes

**Shortcut:** If app is running, `GET /openapi.json` returns the auto-generated spec → Mode B.

### TypeScript — NestJS
- `*.dto.ts` → `@ApiProperty` decorators (field + description + example pre-written)
- `*.controller.ts` → `@ApiOperation`, route decorators
- `enums/*.ts` → enum definitions

**Jackpot:** `@ApiProperty({ description: '...', enum: TransferStatus })` = ready to use.

### TypeScript — Express + Zod/Joi
- `*.schema.ts` → Zod schema (`.optional()` = not required; `z.enum([...])` = enum values)
- `*.routes.ts` → route definitions
- `*.types.ts` → TypeScript interfaces

Zod example: `amount: z.number().positive().max(1000000)` → type: number, min: 0.01, max: 1000000

### Ruby on Rails
- `*_serializer.rb` → exposed fields
- `models/*.rb` → `enum status: { pending: 'pending', ... }` + validations
- `controllers/api/v*/*.rb` → strong params (permitted = valid request fields)

### Go
- `handler.go` → route registration
- `model.go` → struct `json:"field_name"` tags (omitempty = optional in response)

### Java — Spring Boot
- `*DTO.java` → `@JsonProperty("field_name")` (use annotation value, not Java field name)
- `*Controller.java` → `@PostMapping`, `@RequestBody`
- `enums/*.java` → enum constants

---

## What to Extract (Universal)

**From route files:**
```
Path: /api/v2/transfers/batch
Method: POST
Auth: BearerAuth (from permission class / middleware)
Rate limit: (from @ratelimit / throttle_classes if present)
```

**From serializer/schema files:**
```
Field      | Type   | Required | Constraints       | Source line
amount     | float  | YES      | >0, max:1M        | serializer.py:14
currency   | string | YES      | enum:INR,USD,GBP  | serializer.py:18
note       | string | NO       | max:140           | serializer.py:22
```

**From enum files:**
```
TransferStatus:
  pending     → queued, not yet processing
  processing  → submitted to payment network
  settled     → completed, funds received
  failed      → rejected or errored
```

**From test fixtures:**
```
Golden request: { "amount": 5000.00, "currency": "INR", ... }
Golden response: { "id": "uuid", "status": "pending", ... }
```

---

## Codebase Intelligence Pack Output

```
╔══════════════════════════════════════════════╗
  CODEBASE INTELLIGENCE PACK
  Framework: [framework] | Files read: [n]
╠══════════════════════════════════════════════╣
FOR EACH API-CHANGE TICKET:
  [PROJ-ID] → [METHOD /path]
  Endpoint facts: [auth, rate limit, path params]
  Request schema: [field table]
  Response schema: [field table]
  Enums: [all values + meanings]
  Golden examples: [from tests / CONSTRUCTED]
  
EXISTING SPEC: [Found v2.2 / Not found]
CONFIDENCE: [HIGH/MEDIUM/LOW per ticket]
VERIFY FLAGS: [list any unresolved]
╚══════════════════════════════════════════════╝
```

**Never invent field names.** Missing = `[VERIFY WITH ENGINEER: field not found in source]`

---

## Fintech-Specific Checks

```
☑ IDEMPOTENCY: Idempotency-Key middleware present on state-changing endpoints?
☑ CURRENCY: Amounts as integers (paise/cents) or floats? Document clearly.
☑ RATE LIMITING: throttle_classes / @ratelimit present? → document 429 response
☑ WEBHOOKS: Outbound webhooks triggered? → document payload shape as separate schema
