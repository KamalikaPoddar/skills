# PM Technical Writer

> **Turn sprint output into polished documentation — release notes, OpenAPI specs,
> feature guides, and changelogs — with codebase-accurate YAML when running in
> Claude Code or Cursor.**

A multi-agent skill for AI-native product managers. Ingests from Jira, Notion,
Confluence, uploads, and — when running in Claude Code or Cursor — reads your actual
codebase to produce OpenAPI 3.0 YAML that reflects reality, not guesswork.

Built by [Kamalika Poddar](https://github.com/kamalikap) — 12 years building fintech
infrastructure across core banking, UPI, payment aggregators, account aggregators,
and cross-border payment rails.

---

## The Core Problem This Solves

API documentation has a fundamental accuracy problem: you can't produce correct field
names, enum values, and response codes without the source that defines them. Most AI
doc tools either skip this (producing skeletons with invented fields) or require
expensive custom integrations.

This skill solves it with a **4-mode progressive accuracy system** — using whatever
sources are available, being honest about confidence, and never inventing details it
can't verify.

---

## Architecture — Four Layers, Eight Agents

```
LAYER 1 — INGESTION
  1A  Ticket Ingestion   Jira / Notion / Confluence / upload / paste
  1B  Codebase Reader    Route files, serializers, enums, tests, PR diffs
                         ← Primary path: Claude Code / Cursor
  1C  Spec Reader        Existing openapi.yaml, Postman, Insomnia

LAYER 2 — CLASSIFICATION & ROUTING
  2   Ticket Classifier  Types every ticket; flags API Change, Breaking, No-Doc
  3   API Intelligence   Merges all sources; declares Mode A–D

LAYER 3 — WRITING (parallel, audience-split)
  4   Release Notes      External customer-facing
  5   Feature Doc        How-to guides for end users
  6   OpenAPI YAML       Mode-dependent spec output
  7   Internal Changelog Dev / ops / support facing

LAYER 4 — QA
  8   QA & Review        Validates all. Hard blocks on unresolved [VERIFY] flags.
```

---

## The Four YAML Accuracy Modes

| Mode | What's available | Accuracy | Publish-safe? |
|---|---|---|---|
| **A** | Codebase files (Claude Code/Cursor) | 95%+ | Yes, after PM review |
| **B** | Existing openapi.yaml + ticket delta | 85–90% | Yes, engineer sign-off |
| **C** | PR diff/description + ticket | 70–80% | After engineer verifies |
| **D** | Ticket data only | 40–60% skeleton | No — engineer review |

Agent 3 (API Intelligence) detects mode, announces it with a **Mode Declaration**
before writing any YAML, and marks uncertain fields `[VERIFY WITH ENGINEER]`.
Agent 8 (QA) hard-blocks publishing until all flags are resolved.

---

## Why Claude Code / Cursor Is the Primary Path

In Claude Code or Cursor, Agent 1B reads your source files directly:

- **Serializer / schema / DTO files** → exact field names, types, validators
- **Enum files** → all valid values and runtime meanings
- **Route / controller files** → paths, methods, auth, permissions
- **Test / fixture files** → real examples for YAML `example` fields
- **Migration files** → what schema changed this sprint

**Supported frameworks:** Django REST Framework, FastAPI, NestJS, Express + Zod/Joi,
Rails + ActiveModelSerializers, Spring Boot, Go.

In Claude.ai web (no filesystem), the skill falls back gracefully — asks for paste,
runs in Mode B/C/D, marks all uncertain fields clearly.

---

## What Gets Produced

| Document | Audience | Trigger |
|---|---|---|
| External Release Notes | Customers | Any user-visible change |
| Feature How-To Guide | End users / admins | New Feature or Enhancement |
| OpenAPI 3.0 YAML | Developers / integrators | Any API Change ticket |
| API Changelog (human-readable) | Developers | Any API Change |
| Internal Changelog | Ops / engineering / support | Every sprint |
| QA Review Report | PM before publishing | Every session |

---

## File Structure

```
pm-technical-writer/
├── SKILL.md
├── README.md
└── references/
    ├── source-ingestion.md           # Agent 1A
    ├── codebase-reader.md            # Agent 1B — framework reading patterns
    ├── spec-reader.md                # Agent 1C
    ├── ticket-classifier.md          # Agent 2
    ├── api-intelligence.md           # Agent 3 — mode logic + Mode Declaration
    ├── api-doc-writer.md             # Agent 6
    ├── feature-doc-writer.md         # Agent 5
    └── templates/
        ├── release-notes-template.md
        └── openapi-stub-template.yaml
```

---

## Quick Start

### Claude Code (Mode A — Full Accuracy)

```
# In your project root:
claude

# In conversation:
"Document Sprint 24. I need release notes and API docs."

# Skill fetches Jira, reads your serializer/route files,
# declares Mode A, generates accurate YAML, produces full doc pack.
```

### Claude.ai Web (Mode B/C/D)

```
"Write release notes for this sprint: [paste tickets]
 Here's the serializer for the new endpoint: [paste file]"

# Skill classifies tickets, declares mode based on what you've provided,
# produces docs with [VERIFY] flags for anything it can't confirm.
```

### Common Flows

```
Release notes only:      1A → 2 → 4 → 8
Feature doc only:        1A → 2 → 5 → 8
API docs (Claude Code):  1A → 1B → 1C → 2 → 3 → 6 → 7 → 8
Full sprint:             All 8 agents → complete document pack
```

---

## The Never-Invent Rule

This skill never fabricates field names, enum values, types, or response codes.
If a detail can't be sourced from code, an existing spec, a PR diff, or the ticket,
it is marked `[VERIFY WITH ENGINEER]` and the QA agent blocks publishing until
resolved. A skeleton with honest gaps is more useful than a complete spec with
wrong field names.

---

## Roadmap

- [ ] GitHub PR MCP for Mode C auto-fetch
- [ ] Confluence write-back (publish directly)
- [ ] Swagger Editor validation pass on generated YAML
- [ ] Multi-sprint diff ("what changed v2.2 → v2.3?")

---

## Author

**Kamalika Poddar** · [GitHub](https://github.com/kamalikap) · [LinkedIn](https://linkedin.com/in/kamalikap)

MIT License
