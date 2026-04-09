# Design-Log Schema Reference

Full field reference for YSH Store Design-Log entries. Source of truth: `design-log/schema.json`.

---

## Required Fields

All entries **must** include these fields:

| Field | Type | Description |
|-------|------|-------------|
| `id` | `string` | Unique ID. Format: `DL-NNN` (e.g., `DL-001`, `DL-042`) |
| `title` | `string` | Short descriptive title. Min 5, max 120 chars |
| `status` | `enum` | Lifecycle status (see table below) |
| `date` | `string` | ISO 8601 date (e.g., `2026-04-09`) |
| `domain` | `enum` | Primary domain (see table below) |
| `impact` | `enum` | Impact level: `baixo` \| `médio` \| `alto` \| `crítico` |
| `context` | `string` | Background: what is happening, why is this decision needed now? Min 20 chars |
| `problem` | `string` | Specific problem or gap that needs to be addressed. Min 10 chars |
| `decision` | `string` | What was decided — be specific and precise. Min 10 chars |

---

## Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `affected_files` | `string[]` | Files or modules directly impacted |
| `supersedes` | `string` | ID of the entry this one replaces (e.g., `DL-002`) |
| `related` | `string[]` | IDs of related entries (e.g., `["DL-001", "DL-003"]`) |
| `approach` | `string` | Implementation guidance — which files, what sequence |
| `alternatives_considered` | `object[]` | Each: `{ option, reason_rejected }` |
| `success_criteria` | `string[]` | Measurable proof of completion |
| `consequences` | `object` | `{ positive: string[], negative: string[] }` |
| `evidence` | `object` | `{ pr_url, commit_sha, test_output, notes }` — required for `done` status |
| `agents_rule_derived` | `string` | New rule added to `AGENTS.md` derived from this entry |

---

## Status Values

| Status | Meaning | Agent authority |
|--------|---------|----------------|
| `draft` | Being written | None |
| `review` | Pending human approval | None |
| `approved` | Approved, not yet started | **BINDING** |
| `executing` | Actively being implemented | **BINDING** |
| `done` | Completed with evidence | Reference |
| `rejected` | Not adopted | Ignore |
| `superseded` | Replaced by newer entry | Ignore |

---

## Domain Values

| Domain | Scope |
|--------|-------|
| `plataforma` | Core stack, repo structure, monorepo, tooling |
| `catálogo` | Product catalog, solar panel families, variants, pricing |
| `agente` | AI agent rules, AGENTS.md, skills, plugins |
| `stack` | Technology choices (Medusa v2, Next.js 15, pnpm, etc.) |
| `lifecycle` | Deployment pipeline, environments, CI/CD, branches |
| `sistema` | Cross-cutting concerns, shared modules, architecture patterns |
| `segurança` | Authentication, authorization, secrets, permissions |
| `observabilidade` | Logging, monitoring, tracing, error reporting |
| `ux` | UI/UX decisions, component design, user flows |
| `integração` | External APIs, webhooks, third-party services |
| `testes` | Testing strategy, Vitest, coverage thresholds, E2E |

---

## Impact Values

| Value | Meaning |
|-------|---------|
| `baixo` | Minimal impact — localized change |
| `médio` | Moderate impact — affects a module or feature |
| `alto` | High impact — affects multiple modules or user-facing behavior |
| `crítico` | Critical impact — affects core architecture or platform stability |

---

## Frontmatter vs Markdown Body

A design-log entry is a Markdown file. The YAML frontmatter contains the structured fields above. The Markdown body **mirrors** the frontmatter with human-readable prose sections:

```markdown
---
id: DL-NNN
title: ...
status: draft
date: YYYY-MM-DD
domain: plataforma
impact: médio
...
---

## Context
[prose version of context field]

## Problem
[prose version of problem field]

## Decision
[prose version of decision field]

## Approach
[optional — implementation guidance]

## Alternatives Considered
[optional]

## Success Criteria
[optional]

## Consequences
[optional]

## Evidence
[required when status = done]
```

Both the frontmatter and the Markdown sections should be kept in sync.
