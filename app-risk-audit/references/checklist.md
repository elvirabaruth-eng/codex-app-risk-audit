# App Risk Audit Checklist

Use this checklist as the audit baseline.

## Security

1. Injection
   - SQL injection through dynamic queries, table names, columns, filters, order clauses.
   - Command injection through shell/process calls, file paths, archive extraction, image/document tools.
   - Check whether dynamic identifiers are whitelisted and values are parameterized.

2. Authentication and authorization
   - Missing role checks, weak session checks, wrong role/session namespace.
   - Object-level authorization: users/viewers/participants must not see foreign company, project, session, response, or task data.
   - Public routes must be token-bound and minimally scoped.
   - Generic CRUD APIs are high-risk and need table, field, method, and row-level constraints.

3. Sensitive data and secrets
   - Password storage: bcrypt/argon preferred; legacy SHA/MD5/plaintext is a risk.
   - API keys, DB credentials, reset tokens, debug tokens, or secrets in frontend or repo.
   - Sensitive fields must not be returned to non-admin clients.

4. XSS and frontend injection
   - `innerHTML`, inline `onclick`, `href`, `mailto`, markdown/HTML rendering, preview/import error rendering.
   - Verify all user-controlled strings pass through escaping.
   - Prefer DOM APIs or textContent for new code.

5. Input validation
   - Required fields, type checks, length limits, enum values, dates, status transitions, numeric ranges.
   - Validate server-side, not only frontend.
   - Import/upload parsers need strict schema checks and row limits.

6. Dependencies and supply chain
   - CDN scripts/styles without SRI.
   - Unpinned dependencies, abandoned packages, missing lockfiles, known CVEs.
   - External scripts should be constrained by CSP where possible.

7. Configuration and deployment hardening
   - Missing CSP, frame protection, HSTS, nosniff, cache rules for sensitive responses.
   - Debug mode or `debug_message` exposed to clients.
   - CORS too broad, public health endpoints with internal detail.
   - Cookie flags: Secure, HttpOnly, SameSite.

## Code Quality and Architecture

8. Structural cleanliness
   - Files with unrelated responsibilities, very large "god files", hidden global state.
   - UI, API, database, and business logic should be separated.
   - New modules should preserve existing public method names if refactoring.

9. No cosmetic fixes
   - Check whether fixes hide symptoms: disabled buttons, swallowed errors, visual-only masking.
   - Prefer root-cause fixes: endpoint, data model, validation, permissions, query shape.

10. No one-off hacks
   - Repeated special cases for similar logic.
   - Status labels, categories, roles, thresholds, table names, and config should be centralized.

11. Consistent data flows
   - Same value calculated in multiple places.
   - Duplicated state across frontend, API, SQL, imports, exports.
   - Import/export schema must match UI, API, and database.

12. Business logic centralization
   - Scheduling, scoring, capacity, status activation, permissions, and report logic should have one authoritative path.
   - Watch for frontend-only enforcement of critical logic.

13. Hidden dependencies
   - Script load order, globals, cache versions, route state, implicit DB columns, missing migrations.
   - Changes in one module should not silently break another.

14. Error handling
   - Avoid empty catch blocks, client-visible stack/DB messages, console-only handling for user-critical failures.
   - Log technical detail server-side; return safe user messages.

15. Edge cases
   - Empty data, missing config, older database schema, deleted resources, duplicate names, invalid dates, circular dependencies, timezone/date rounding.
   - File import preview vs actual import must match.

16. Critical hardcoding
   - Domains, cookie domain, API paths, roles, status strings, table prefixes, category lists, thresholds.
   - Hardcoded values are acceptable only if centralized and documented.

17. Technical debt visibility
   - Temporary migration logic, legacy hashes, deprecated tables, compatibility columns, TODOs.
   - Mark debt with priority and removal conditions.

## Product Problems Observed in This App Build

Include these checks when relevant to any app:

- Long page navigation due to over-fetching, repeated full-table loads, missing server filters, or excessive client rendering.
- Database tables or columns missing after frontend features are added; setup/migration scripts must be idempotent.
- UUIDs leaking into user-facing UI where labels/names should be shown.
- Encoding/locale issues: umlauts, mojibake, inconsistent display strings.
- Import/export templates drifting from current schema or business logic.
- Dependencies between tasks/items calculated inconsistently; schedule recalculation overriding fixed manual dates.
- Resource/capacity logic incorrectly splitting effort or double-counting shared meetings.
- Dashboard and detail views showing duplicate or unnecessary data.
- Status automation causing unclear workflow state.
- Cache-busting version not updated after split JS files.
- Large modules split without checking script order and global method availability.
- Public generic APIs used where a narrow token-bound endpoint is safer.
