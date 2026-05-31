---
dashboard:
  schema_version: 1
  notes: "Reusable Codex skill for structured application risk audits."
  short_note: RiskAudit

  project:
    id: codex-app-risk-audit
    title: Codex App Risk Audit
    status: active
    description: "Reusable Codex skill package for app risk audits"
    owner: local

  lifecycle:
    cycle_id: v1
    version: 1.0.0
    started_at: "2026-05-15"
    completed_at:
    baseline:
      code_chars: 9841
      code_lines: 215
      created_at: "2026-05-15T00:00:00+02:00"
      note: "Initial VC Dashboard baseline after plan bootstrap"
    archived_versions: []

  github:
    enabled: true
    repo: elvirabaruth-eng/codex-app-risk-audit
    url: https://github.com/elvirabaruth-eng/codex-app-risk-audit
    branch: main
    last_push_at:

  code:
    include_extensions:
      - .md
      - .yaml
      - .yml
      - .json
    exclude_paths:
      - node_modules
      - .git
      - dist
      - build
      - coverage
      - .next
      - vendor
      - storage
      - .cache
      - data/snapshots
    exclude_files:
      - package-lock.json
      - pnpm-lock.yaml
      - yarn.lock

  progress:
    percent: 60
    done: 3
    total: 5
    code_chars_at_100_percent:
    code_lines_at_100_percent:

  current_phase:
    id: P2
    title: Checklist Review
    status: active

  phases:
    - id: P1
      title: Skill Package Baseline
      status: completed
      done: 2
      total: 2
      started_at: "2026-05-15"
      completed_at: "2026-05-15"
      target_at:
      note: "README, SKILL.md, OpenAI agent metadata, and checklist reference are present"
    - id: P2
      title: Checklist Review
      status: active
      done: 1
      total: 2
      started_at: "2026-05-15"
      completed_at:
      target_at:
      note: "Review checklist completeness and practical risk coverage"
    - id: P3
      title: Install And Usage Notes
      status: pending
      done: 0
      total: 1
      started_at:
      completed_at:
      target_at:
      note: "Confirm installation notes stay portable across local Codex skill directories"

  risks:
    - id: R1
      title: Checklist may be too broad for small apps
      probability: medium
      impact: medium
      mitigation: "Keep findings prioritized and allow scope-based exclusions in audit output"
      status: open
    - id: R2
      title: Skill instructions may drift from Codex workflow rules
      probability: low
      impact: medium
      mitigation: "Review SKILL.md when global workflow or agent routing changes"
      status: open

  next_steps:
    - title: Review checklist for missing real-world app risks
      priority: high
      status: open
    - title: Add examples only after checklist scope is stable
      priority: medium
      status: open
---

# Codex App Risk Audit Plan

## Ziel

Dieses Repository pflegt eine wiederverwendbare Codex-Skill fuer strukturierte Risiko-Audits von Anwendungen. Der Fokus liegt auf einer praktisch nutzbaren Checkliste fuer Security, Architektur, Datenfluss, Wartbarkeit, API-, Datenbank-, Frontend-, Import/Export-, Dependency- und Konfigurationsrisiken.

## Arbeitsstand

- Skill-Paket liegt unter `app-risk-audit/`.
- `SKILL.md` beschreibt Zweck und Ausloeser.
- `references/checklist.md` enthaelt die Audit-Checkliste.
- `agents/openai.yaml` enthaelt optionale Agent-Metadaten.

## Naechster Fokus

Die Checkliste soll auf Vollstaendigkeit, Praktikabilitaet und sinnvolle Strenge geprueft werden. Neue Beispiele oder Erweiterungen sollten erst danach ergaenzt werden.
