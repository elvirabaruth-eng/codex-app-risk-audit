# Codex App Risk Audit Skill

Reusable Codex skill for auditing applications for security, architecture, data-flow, maintainability, API, database, frontend, import/export, dependency, and configuration risks.

## Contents

```text
app-risk-audit/
  SKILL.md
  agents/
    openai.yaml
  references/
    checklist.md
```

## Usage

Copy `app-risk-audit/` into a Codex skills directory, for example:

```powershell
Copy-Item -Recurse .\app-risk-audit C:\Users\<user>\.agents\skills\app-risk-audit
```

Then invoke it with:

```text
Use $app-risk-audit to analyze this application and return a prioritized findings table.
```

## Review Focus

Please review whether the checklist is complete, too strict, too broad, or missing practical real-world app risks.
