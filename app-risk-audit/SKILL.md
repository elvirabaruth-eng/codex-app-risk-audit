---
name: app-risk-audit
description: Audit any application or repository for security, architecture, data-flow, maintainability, performance, database, API, frontend, import/export, configuration, and AI-generated-code risks. Use when the user asks to analyze an app, check code quality, assess typical AI-code security issues, rank open risks by criticality, or produce a findings table before implementing fixes.
---

# App Risk Audit

## Goal

Run a structured risk audit on an arbitrary app and return a concise table with severity, evidence, impact, and recommendations. Do not change code unless the user explicitly asks for fixes.

## Workflow

1. Inspect governance first: nearest `AGENTS.md`, README, contributor/release docs, framework config, package files, API entry points, database migrations/setup, and route/bootstrap files.
2. Map the app surface:
   - frontend entry points, routers, views, state/data loading
   - backend endpoints, auth/session middleware, table/API abstractions
   - database tables, migrations, relationships, required fields
   - imports/exports, file upload/parsing, background/batch endpoints
   - external libraries/CDNs/build/deploy configuration
3. Check the standard risk categories in `references/checklist.md`.
4. Rank each finding by exploitability and business impact, not by how easy it is to fix.
5. Separate proven findings from assumptions. If something cannot be verified locally, mark it as "Nicht verifiziert" and explain what would prove it.
6. Return a table first. Add a short priority summary after the table.

## Search Guidance

Use fast repository searches before reading large files:

```bash
rg -n "prepare\\(|query\\(|exec\\(|shell_exec|system\\(|passthru\\(|eval\\(|innerHTML|insertAdjacentHTML|debug_message|password_hash|password_verify|csrf|role|admin|viewer|public|Access-Control|Content-Security-Policy|api[_-]?key|secret" .
rg --files
```

For web/PHP apps, inspect:

- API/router entry files
- auth/session helpers
- generic CRUD/table APIs
- import/export endpoints
- setup/migration scripts
- frontend API client
- files that render `innerHTML`
- dependency declarations or CDN script tags

## Output Format

Use this table shape unless the user asks otherwise:

| Nr. | Bereich | Befund | Kritikalität | Beleg/Fundstelle | Auswirkung | Empfehlung |
|---:|---|---|---|---|---|---|

Severity scale:

- **Kritisch**: likely unauthorized data exposure, data manipulation, auth bypass, credential leak, RCE/command injection, destructive production risk.
- **Hoch**: plausible XSS in privileged context, debug info leak, broken object-level authorization, weak server validation affecting business logic.
- **Mittel**: missing hardening, weak legacy crypto fallback, CDN/SRI/CSP risk, maintainability issue that can produce bugs or inconsistent data.
- **Niedrig**: cosmetic, documentation, minor configuration, or low-impact operational issue.

## Review Rules

- Prefer exact file/line references.
- Do not report generic theoretical issues unless the code surface exists.
- Mention existing protections, not only weaknesses.
- Include "keine Codeänderung durchgeführt" when only analyzing.
- If asked to update a previous analysis table, preserve completed items and update statuses rather than rewriting history.

## References

Read `references/checklist.md` when performing the audit.
