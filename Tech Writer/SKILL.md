---
name: pm-technical-writer
description: >
  The PM Technical Writer. Invoke this skill whenever a product manager needs to
  produce release notes, feature documentation, API specs, or changelogs from sprint
  output. Triggers on: "write release notes", "document this sprint", "create release
  notes from Jira", "write API docs", "generate OpenAPI YAML", "update the changelog",
  "document this feature", "write a user guide for", "what shipped this sprint",
  "help me document what we built", "document what we released", "create setup and
  configuration guide", "write technical documentation", or any variation where a PM
  needs to translate engineering work into user-facing or developer-facing documentation.
  Also triggers when a PM pastes Jira tickets, a PRD, or a sprint summary and asks
  "what do I need to document?" or "turn these tickets into release notes". This skill
  covers the complete technical writer workflow across four layers: ingestion →
  classification → writing → QA. Always invoke at the start of any documentation session.
---

# PM Technical Writer

A multi-agent skill that turns sprint output into polished, audience-correct
documentation. It ingests from Jira, Notion, Confluence, uploaded files, and — when
running in Claude Code or Cursor — reads codebases directly to produce accurate
OpenAPI 3.0 YAML without guesswork.

---

## Architecture — Four Layers, Eight Agents

```
╔══════════════════════════════════════════════════════════════════════╗
║  LAYER 1 — INGESTION                                                 ║
║                                                                      ║
║  Agent 1A │ Ticket Ingestion      Jira / Notion / Confluence /       ║
║           │                       upload / paste                     ║
║           │                                                          ║
║  Agent 1B │ Codebase Reader       Route files, serializers, schemas, ║
║           │ (Claude Code primary) enums, tests, PR diffs             ║
║           │                                                          ║
║  Agent 1C │ Spec Reader           Existing openapi.yaml, Postman     ║
║           │                       collection, Insomnia export        ║
╠══════════════════════════════════════════════════════════════════════╣
║  LAYER 2 — CLASSIFICATION & ROUTING                                  ║
║                                                                      ║
║  Agent 2  │ Ticket Classifier     Types every ticket, flags API       ║
║           │                       changes and breaking changes       ║
║           │                                                          ║
║  Agent 3  │ API Intelligence      Merges ticket + code + spec data.  ║
║           │                       Declares operating mode (A–D).     ║
║           │                       Flags gaps before writing starts.  ║
╠══════════════════════════════════════════════════════════════════════╣
║  LAYER 3 — WRITING  (parallel, audience-split)                       ║
║                                                                      ║
║  Agent 4  │ Release Notes Writer  External customer-facing           ║
║  Agent 5  │ Feature Doc Writer    How-to guides for end users        ║
║  Agent 6  │ OpenAPI YAML Writer   Spec output — mode-dependent       ║
║  Agent 7  │ Internal Changelog    Dev / ops / support facing         ║
╠══════════════════════════════════════════════════════════════════════╣
║  LAYER 4 — QA                                                        ║
║                                                                      ║
║  Agent 8  │ QA & Review           Validates all outputs. Blocks      ║
║           │                       publication on unresolved flags.   ║
╚══════════════════════════════════════════════════════════════════════╝
```

---

## Step 0 — Environment Detection

Before running any agent, detect the runtime environment:

```
Am I running inside Claude Code or Cursor (filesystem access available)?
  YES → CODEBASE ACCESS MODE
        - Agent 1B reads files directly
        - Agent 3 defaults to Mode A (Full Spec Generation)
        - Tell PM: "I can read your codebase directly. Point me to the
          relevant files or I'll find them."

  NO → WEB / CHAT MODE
        - Agent 1B requests paste or upload
        - Agent 3 determines best available mode (B, C, or D)
        - Tell PM: "For accurate API docs, paste your serializer/schema
          file or share your existing openapi.yaml."
```

---

## Step 1 — Understand the Request

Determine:
1. **Source** — Jira sprint / uploaded PRD / paste / Confluence link / codebase
2. **Output needed** — release notes / feature docs / API YAML / all
3. **Audience** — customers / developers / internal ops / all
4. **Release scope** — version / sprint name / date range

If unclear, ask in ONE message — three questions maximum.

---

## Layer 1: Ingestion Agents

### Agent 1A — Ticket Ingestion

Read: `references/source-ingestion.md`

Pulls from: Jira MCP, Notion MCP, Confluence MCP, Google Docs MCP, file upload, paste.

Output: **Normalized Ticket List** — every ticket with ID, title, description,
type, status, acceptance criteria, tech notes, API keywords.

---

### Agent 1B — Codebase Reader

Read: `references/codebase-reader.md`

**This is the accuracy engine. Run it whenever any ticket is flagged as API Change.**

Primary path: Claude Code / Cursor (filesystem access)
Fallback: paste or upload of specific files

Reads only the files needed — not the whole codebase:
- Route / controller files → endpoint paths, HTTP methods, auth middleware
- Serializer / schema / DTO files → exact field names, types, required flags
- Enum / constant files → all valid values and their runtime meanings
- Model / entity files → field constraints, nullable flags
- Test / fixture files → golden request+response examples
- Migration files → what schema changed this sprint
- PR diff → the precise delta from last version

Output: **Code Intelligence Pack** — ground truth for every changed endpoint.

---

### Agent 1C — Spec Reader

Read: `references/spec-reader.md`

Reads existing API spec if available:
- `openapi.yaml` / `openapi.json` in the repo (Claude Code: auto-locate)
- Postman collection export (JSON)
- Insomnia workspace export (JSON)
- Swagger 2.0 spec (auto-converts structure)

Output: **Existing Spec Summary** — what's already documented, at what version,
which paths exist, flagging any paths referenced in new tickets.

---

## Layer 2: Classification & Routing

### Agent 2 — Ticket Classifier

Read: `references/ticket-classifier.md`

Classifies every ticket:

| Type | Definition | Doc impact |
|---|---|---|
| **New Feature** | Net-new user capability | Feature doc + release note + (API?) YAML |
| **Enhancement** | Improvement to existing feature | Release note + update existing doc |
| **Bug Fix** | Corrects unintended behaviour | Release note (if user-visible) |
| **Tech Debt** | Internal refactor / infra / cleanup | Internal changelog only |

Secondary flags: `API Change` / `Breaking Change` / `No-Doc`

Output: **Classified Inventory** table.

---

### Agent 3 — API Intelligence

Read: `references/api-intelligence.md`

**The synthesis layer.** Merges ticket data + Code Intelligence Pack + Existing Spec
Summary → decides how to proceed → issues a Mode Declaration.

**Four operating modes:**

| Mode | Sources available | YAML quality | Publish-safe? |
|---|---|---|---|
| **A — Full Generation** | Codebase files + ticket | 95%+ accurate | Yes, after PM review |
| **B — Spec Enrichment** | Existing spec + ticket | 85–90% accurate | Yes, with engineer sign-off on new fields |
| **C — PR-Informed Stub** | PR diff/description + ticket | 70–80% accurate | After engineer verifies new fields |
| **D — Skeleton** | Ticket data only | 40–60% structural | No — needs full engineer review |

Issues a **Mode Declaration** before any YAML is written:
```
API INTELLIGENCE REPORT
═══════════════════════
Endpoint: POST /api/v2/transfers/batch
Mode: B — Spec Enrichment
Sources: openapi.yaml v2.2 + PROJ-104

Confidence: HIGH for existing fields | MEDIUM for 3 new fields from ticket

Gaps requiring engineer input before publishing:
  [VERIFY] batchStatus enum — ticket says "queued/processing" — are
           "cancelled" and "expired" also valid runtime states?
  [VERIFY] maxBatchSize — "up to 100" from ticket — is this a 400 or 422?
```

Mode D must always include a prominent warning:
```
⚠️ SKELETON MODE — This YAML was generated from ticket data only.
   Every field name, type, and enum value marked [VERIFY] must be
   confirmed against the actual codebase before publishing.
   Do not merge into your spec without engineer review.
```

---

## Layer 3: Writing Agents

### Agent 4 — Release Notes Writer

Read: `references/templates/release-notes-template.md`

Rules:
- User-benefit led — "You can now..." not "We implemented..."
- Zero ticket IDs in external notes
- "Various improvements" always rejected
- Breaking changes always first, with migration steps
- Structure: ⚠️ Breaking | ✨ New | 🔧 Improvements | 🐛 Fixes | 🔒 Security

---

### Agent 5 — Feature Doc Writer

Read: `references/feature-doc-writer.md`

Produces how-to documentation: overview, prerequisites, setup steps, configuration
reference, worked example, FAQ, known limitations, troubleshooting.

One action per step. Names UI elements exactly as they appear. Never invents
field names not found in source material.

---

### Agent 6 — OpenAPI YAML Writer

Read: `references/api-doc-writer.md`

Produces OpenAPI 3.0 YAML path blocks ready to merge into `openapi.yaml`.
Behaviour is entirely determined by the mode declared by Agent 3:

- **Mode A:** Generates complete, accurate YAML from codebase files
- **Mode B:** Generates delta YAML (new/changed paths only) against existing spec
- **Mode C:** Generates mostly-accurate stub, marks uncertain fields `[VERIFY]`
- **Mode D:** Generates structural skeleton, marks all fields `[VERIFY WITH ENGINEER]`

Also produces a human-readable **API Changelog block** alongside the YAML.

---

### Agent 7 — Internal Changelog Writer

Read: `references/templates/release-notes-template.md` (internal section)

Audience: engineering, DevOps, support. Full technical detail.

Covers: new/modified/deprecated endpoints, database schema changes, breaking changes
with migration steps and deadlines, infrastructure changes, tech debt resolved,
security fixes (full internal detail), known issues with workarounds.

---

## Layer 4: QA

### Agent 8 — QA & Review Agent

Runs automatically after all writing agents complete.

**Hard blocks — will NOT pass until resolved:**
- Any `[VERIFY WITH ENGINEER]` or `[VERIFY]` flag in YAML output
- Any `[NEEDS SME INPUT]` flag in any document
- Breaking change present but no migration steps written
- Any external document containing a Jira ticket ID

**Warnings — flagged but not blocking:**
- "Various improvements" or "minor fixes" language detected
- API field with empty `description`
- External doc containing technical jargon (>3 per document)
- Feature doc missing Prerequisites or Known Limitations section

Output: per-document PASS ✅ / FIX NEEDED ⚠️ / BLOCKED 🚫 status
plus a specific fix instruction for every issue found.

---

## Quick-Start Flows

**"Write release notes for this sprint"**
```
1A (ingest Jira) → 2 (classify) → 4 (release notes) → 8 (QA)
```

**"Document this new feature"**
```
1A (ingest spec/PRD) → 2 (classify) → 3 (route) → 5 (feature doc) → 8 (QA)
```

**"We added new API endpoints — document them"**
```
1A (ingest ticket) → 1B (read codebase) → 1C (read existing spec)
→ 2 (classify) → 3 (API Intelligence + mode) → 6 (YAML) → 7 (internal CL) → 8 (QA)
```

**"Document everything from this sprint"**
```
Full pipeline → all 8 agents → complete document pack
```

---

## Reference Files

| File | Layer | Agent | Read when |
|---|---|---|---|
| `references/source-ingestion.md` | 1 | 1A | Any session with Jira/Notion/upload |
| `references/codebase-reader.md` | 1 | 1B | Any API Change ticket detected |
| `references/spec-reader.md` | 1 | 1C | Existing spec available or suspected |
| `references/ticket-classifier.md` | 2 | 2 | Every session |
| `references/api-intelligence.md` | 2 | 3 | Any API Change ticket |
| `references/api-doc-writer.md` | 3 | 6 | When producing YAML |
| `references/feature-doc-writer.md` | 3 | 5 | New Feature or Enhancement |
| `references/templates/release-notes-template.md` | 3 | 4, 7 | Release notes + internal CL |
| `references/templates/openapi-stub-template.yaml` | 3 | 6 | YAML generation |
