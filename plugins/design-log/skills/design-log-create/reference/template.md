# Design-Log Entry Template

Copy this template when creating a new design-log entry. Save as `design-log/DL-NNN-slug.md`.

---

```markdown
---
id: DL-NNN
title: "Short descriptive title of the decision"
status: draft
date: YYYY-MM-DD
domain: plataforma
impact: médio
context: |
  Describe the background context here.
  What is the current situation? Why is this decision needed now?
  Include enough detail for an agent or developer who has never seen this code.
problem: |
  What specific problem or gap is being addressed?
  Be concrete — avoid vague statements.
decision: |
  What was decided? Be explicit and precise.
  State exactly what will be done, not just the goal.
affected_files:
  - "path/to/file1.ts"
  - "path/to/file2.tsx"
supersedes: null
related: []
approach: |
  How will this decision be implemented?
  List the files to change, the order of operations, and any patterns to follow.
alternatives_considered:
  - option: "Description of alternative option"
    reason_rejected: "Why this option was not chosen"
success_criteria:
  - "Criterion 1 — measurable and verifiable"
  - "Criterion 2 — measurable and verifiable"
consequences:
  positive:
    - "Positive outcome 1"
    - "Positive outcome 2"
  negative:
    - "Tradeoff or risk 1"
evidence: null
agents_rule_derived: null
---

## Context

[Prose version of the context field above. Write in full sentences.]

## Problem

[Prose version of the problem field above.]

## Decision

[Prose version of the decision field above.]

## Approach

[Optional — prose version of the approach field. Include code snippets if helpful.]

## Alternatives Considered

[Optional — prose description of alternatives that were evaluated but not chosen.]

## Success Criteria

[Optional — list of measurable criteria that prove this decision was implemented correctly.]

## Consequences

[Optional — what are the positive outcomes and tradeoffs of this decision?]

## Evidence

[Required when status = done. Fill in after completion:]

- PR: [link]
- Commit: [sha]
- Test output: [paste or describe]
- Notes: [any additional context about the implementation]
```

---

## Field removal guide

When creating a real entry, remove optional fields that don't apply:

- Remove `supersedes` if this doesn't replace an existing entry
- Remove `related` if there are no related entries
- Remove `alternatives_considered` if no alternatives were evaluated
- Remove `consequences` if tradeoffs are not yet known
- Leave `evidence: null` until status becomes `done`
- Leave `agents_rule_derived: null` unless a new AGENTS.md rule was created

## Naming convention reminder

- Format: `DL-NNN-short-slug.md`
- NNN: zero-padded 3-digit number (001, 042, 100)
- Slug: lowercase kebab-case, topic-focused
- Examples: `DL-001-platform-foundation.md`, `DL-015-catalog-families.md`
