# Agent 6 — OpenAPI YAML Writer

Produces OpenAPI 3.0 YAML. Quality is entirely governed by Agent 3's Mode Declaration.
**This agent cannot run without a Mode Declaration from Agent 3.**

The mode determines what gets `[VERIFY WITH ENGINEER]` flags vs what goes in cleanly.

---

## Mode Behaviour

| Mode | Field names | Types | Enums | Examples | VERIFY flags |
|------|------------|-------|-------|----------|--------------|
| A — Full Generation | From code | From annotations | From enum class | From test fixtures | Minimal |
| B — Spec Enrichment | From existing spec | From existing spec | From existing spec | Constructed | Only on new fields |
| C — PR-Informed | From diff | From diff | From diff/ticket | Constructed | On unchanged context |
| D — Skeleton | From ticket (unconfirmed) | Inferred | Inferred | Placeholder | On everything |

In Mode D: precede every field name with `# [VERIFY] — from ticket, not confirmed in code`

---

## Full Path Block Template

```yaml
# ──────────────────────────────────────────────
# x-changelog and x-breaking annotations ALWAYS
# present on changed/new endpoints
# ──────────────────────────────────────────────
paths:
  /api/v{n}/{resource}:
    {method}:
      operationId: {camelCaseUniqueId}          # Required. Verb+Resource. E.g. createBatchTransfer
      summary: "{One-line: Verb + what it does}" # ≤10 words
      description: |
        {Full plain-English description.}
        {When to use it. Important behaviours: idempotency, async, pagination.}
        {Added in / modified in vX.Y.}
      tags:
        - {ResourceGroup}
      x-changelog: "{Added|Modified} in v{n} — {one-line description}"
      x-breaking: {true|false}                  # Include only if true

      security:
        - BearerAuth: []

      parameters:
        # Path parameter
        - name: {paramName}
          in: path
          required: true
          description: "{Unique identifier for the [resource]. UUID v4 format.}"
          schema:
            type: string
            format: uuid
            example: "550e8400-e29b-41d4-a716-446655440000"

        # Idempotency key — REQUIRED for any state-changing financial endpoint
        - name: Idempotency-Key
          in: header
          required: true
          description: |
            Client-generated unique key (UUID v4) for safe retries.
            If the same key is submitted twice within 24 hours, the second
            request returns the result of the first without re-processing.
          schema:
            type: string
            format: uuid
            example: "7c9e6679-7425-40de-944b-e07fc1f90ae7"

      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/{RequestSchemaName}'
            example:
              {field1}: {value}
              {field2}: {value}

      responses:
        '200':
          description: "{What success returns and what it means}"
          headers:
            X-Request-ID:
              schema:
                type: string
                format: uuid
              description: Unique identifier for this request. Include in support queries.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/{ResponseSchemaName}'
              example:
                {field1}: {value}
                {field2}: {value}

        '400':
          description: "Bad request — {specific triggers: missing required field, invalid format}"
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
              example:
                error: "VALIDATION_ERROR"
                message: "amount must be greater than 0"
                field: "transfers[0].amount"
                requestId: "550e8400-e29b-41d4-a716-446655440000"

        '401':
          description: "Unauthorized — missing or invalid Bearer token"
        '403':
          description: "Forbidden — token valid but insufficient scope for this operation"
        '404':
          description: "Not found — {resource} with given ID does not exist"
        '409':
          description: "Conflict — {specific conflict: duplicate idempotency key with different payload}"
        '422':
          description: "Unprocessable entity — {specific: amount exceeds daily limit, unsupported currency}"
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
              example:
                error: "LIMIT_EXCEEDED"
                message: "Daily transfer limit of INR 10,00,000 exceeded"
                requestId: "550e8400-e29b-41d4-a716-446655440000"
        '429':
          description: "Rate limit exceeded — {n} requests/{window}. Retry after {Retry-After} seconds."
          headers:
            Retry-After:
              schema:
                type: integer
              description: Seconds to wait before retrying.
        '500':
          description: "Internal server error — unexpected failure. Include X-Request-ID when contacting support."
```

---

## Schema Block Template

```yaml
components:
  schemas:

    {SchemaName}:
      type: object
      required:
        - {required_field_1}
        - {required_field_2}
      properties:

        # String field
        {stringField}:
          type: string
          description: "{What this contains. Exact format. Constraints.}"
          minLength: {n}
          maxLength: {n}
          example: "{realistic_value}"

        # Enum field — ALWAYS list all values with meanings
        {enumField}:
          type: string
          description: |
            {What this represents}.
            Values:
            - `{value1}` — {plain-English meaning}
            - `{value2}` — {plain-English meaning}
            - `{value3}` — {plain-English meaning}
          enum:
            - {value1}
            - {value2}
            - {value3}
          example: "{value1}"

        # Number (financial amount)
        {amountField}:
          type: number
          format: double
          description: "{Amount in [currency]}. Always positive. Maximum 2 decimal places. [Units: paise/cents/base if integer]"
          minimum: 0.01
          example: 1234.50

        # ISO datetime
        {datetimeField}:
          type: string
          format: date-time
          description: "{What this timestamp represents}. ISO 8601 format, UTC timezone."
          example: "2024-01-15T10:30:00Z"

        # UUID
        {idField}:
          type: string
          format: uuid
          description: "Unique identifier for {resource}. Use for status tracking and support queries."
          example: "f47ac10b-58cc-4372-a567-0e02b2c3d479"

        # Currency code
        currency:
          type: string
          description: "ISO 4217 three-letter currency code."
          enum: [INR, USD, GBP, EUR, SGD, AED]   # Use actual supported values from enum file
          example: "INR"

        # Array of objects
        {arrayField}:
          type: array
          description: "{What items this array contains}."
          items:
            $ref: '#/components/schemas/{ItemSchema}'
          minItems: 1
          maxItems: 100

        # Deprecated field
        {deprecatedField}:
          type: string
          deprecated: true
          description: |
            **DEPRECATED as of v{version}.** Use `{newField}` instead.
            This field will be removed in v{removalVersion} ({date}).
          example: "{legacy_value}"

    # Standard error response — shared across all endpoints
    ErrorResponse:
      type: object
      required: [error, message]
      properties:
        error:
          type: string
          description: "Machine-readable error code. SCREAMING_SNAKE_CASE."
          example: "INSUFFICIENT_BALANCE"
        message:
          type: string
          description: "Human-readable explanation. Suitable for logging. Not for display to end users."
          example: "Account balance of INR 500.00 is insufficient for transfer of INR 1,200.00"
        field:
          type: string
          description: "Request field that caused the error, if applicable."
          example: "transfers[0].amount"
        requestId:
          type: string
          format: uuid
          description: "Unique identifier for this request. Include when contacting support."
          example: "550e8400-e29b-41d4-a716-446655440000"

  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
      description: "JWT access token. Obtain from POST /auth/token."
```

---

## Deprecation Patterns

### Deprecating an endpoint (keep it in spec, mark deprecated)
```yaml
/api/v1/payments:
  post:
    deprecated: true
    summary: "[DEPRECATED] Use POST /api/v2/transfers instead"
    description: |
      **Deprecated as of v2.3.** This endpoint will be removed in v3.0 ({date}).

      Migrate to `POST /api/v2/transfers`.
      Migration guide: {link}

      All existing integrations will continue to work until the removal date.
    x-changelog: "Deprecated in v2.3 — use /api/v2/transfers"
    x-breaking: true
```

---

## API Changelog Block (produced alongside YAML)

Human-readable summary for developer docs page:

```markdown
### API Changes — v{version} | {Date}

#### New Endpoints
- `POST /api/v2/transfers/batch` — Submit up to 100 transfers in a single call.
  Returns a `batchId` for polling batch status. [PROJ-104]

#### Modified Endpoints
- `GET /api/v1/users/{id}` — Response now includes `lastLoginAt` (ISO 8601).
  Additive change — existing integrations unaffected. [PROJ-106]

#### Deprecated Endpoints
- `POST /api/v1/payments` — Use `POST /api/v2/transfers`. Removed in v3.0 ({date}).
  Migration guide: {link}. [PROJ-103]

#### Breaking Changes
⚠️ `GET /api/v1/accounts` — `balance` field renamed to `availableBalance`.
  Update all integrations before v2.3 release ({date}). [PROJ-108]
```

---

## Output Checklist (Agent 8 will verify these)

- [ ] Mode Declaration present and matches Agent 3 output
- [ ] Every endpoint: `operationId`, `summary`, `description`, `tags`
- [ ] Every property: non-empty `description` — no blanks
- [ ] Every enum: all values listed with plain-English meanings in description
- [ ] Every response code documented: 200/201, 400, 401, 403, 404, 422, 429, 500
- [ ] At least one request example + one response example per endpoint
- [ ] Idempotency-Key header present on state-changing financial endpoints
- [ ] Breaking changes: `x-breaking: true` + deprecation language
- [ ] New/modified endpoints: `x-changelog` annotation
- [ ] No real PII in examples (synthetic data only)
- [ ] `$ref` targets all defined in `components/schemas`
- [ ] Mode D skeleton: every inferred field has `# [VERIFY]` comment
