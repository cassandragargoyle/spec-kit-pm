# Project Charter — Specification & Template

## Convention

Every project managed with `spec-kit-pm` MUST have a **Project Charter** at `specs/project/<project-id>/project.md` before any planning artifact (Gantt, risks, KPIs, decisions, status reports) is produced for it. The Charter is the canonical record of:

- who authorised the project (Sponsor, source authority),
- who is accountable for it (a single named Project Manager),
- what is in and out of scope,
- what success looks like.

The Charter is the **Initiation gate** for every project. It is enforced by the [PM agent preflight](../../agents/pm.md) and produced as the first step of the [project-initiation workflow](../../workflows/project-initiation.md).

**Why YAML front-matter + Markdown body:**

- Front-matter is mechanically parseable — agents and tooling can validate the gate (`status`, `project_manager`) without reading prose.
- Body holds narrative (goal, scope, constraints, success criteria) for human reading.

## Required Front-matter Fields

| Field | Required | Format | Notes |
| ----- | -------- | ------ | ----- |
| `project_id` | yes | string | Stable, unique within the adopting org. Format not prescribed by the kit. Default suggestion: `<ORG>-<YYYY>-<NNN>` or contract-derived (e.g. `ACME-2026-001`, `CONTRACT-Q4-12345`). |
| `title` | yes | string | Human-readable project title. |
| `status` | yes | enum | One of `draft`, `active`, `paused`, `closed`. The PM agent preflight only honours `active`. |
| `project_manager` | yes | object | `{ name, email }`. Exactly one named person — co-PMs are not permitted. |
| `deputy` | no | object | `{ name, email }`. Optional cover during PM unavailability; not a co-owner. |
| `sponsor` | yes | string | Person or entity authorising the work. |
| `source_authority` | yes | string | Reference to contract, mandate, or formal decision establishing the project. |
| `created` | yes | ISO date | `YYYY-MM-DD`. |
| `updated` | yes | ISO date | `YYYY-MM-DD`. Bumped on every Charter edit. |
| `artifact_directory` | yes | string | Repo-relative path. By convention `specs/project/<project_id>/`. |

## Required Body Sections

Every Charter MUST contain, at minimum:

1. **Goal** — one sentence stating the desired outcome.
2. **Scope** — explicit `In scope` and `Out of scope` lists.
3. **Constraints** — budget, deadline, regulatory, personnel, technical.
4. **Success criteria** — measurable.

Optional but recommended:

- **Stakeholders** — table of name, role, contact.
- **Risks summary** — top 3-5 risks (the full register lives in `risks.md`).
- **Open questions** — for sponsor sign-off.

## Template

Copy the block below into `specs/project/<project-id>/project.md` and fill in.

````markdown
---
project_id: <ORG>-<YYYY>-<NNN>
title: <Human-readable title>
status: draft  # draft | active | paused | closed
project_manager:
  name: <Full name>
  email: <name@example.com>
deputy:
  name: <Optional full name>
  email: <Optional name@example.com>
sponsor: <Person or entity authorising the work>
source_authority: <Contract / mandate / decision reference>
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
artifact_directory: specs/project/<project-id>/
---

# <Project Title>

## Goal

<One sentence stating the desired outcome.>

## Scope

### In scope

- <Item 1>
- <Item 2>

### Out of scope

- <Item 1>
- <Item 2>

## Constraints

- **Budget:** <amount / range / "TBD">
- **Deadline:** <YYYY-MM-DD or milestone>
- **Regulatory:** <relevant regulations / "none">
- **Personnel:** <team size, named roles, dependencies>
- **Technical:** <platform / stack / integration constraints>

## Success criteria

- <Measurable outcome 1>
- <Measurable outcome 2>

## Stakeholders

|Name|Role|Contact|
|---|---|---|
|<…>|<Sponsor>|<…>|
|<…>|<Project Manager>|<…>|

## Open questions

- <Question pending sponsor sign-off>
````

## Rendered Example

```markdown
---
project_id: ACME-2026-001
title: Customer Onboarding Acceleration
status: active
project_manager:
  name: Jane Doe
  email: jane.doe@acme.example
sponsor: Acme VP of Customer Success
source_authority: 2026 OKR commitment, board minutes 2026-Q1
created: 2026-04-15
updated: 2026-04-30
artifact_directory: specs/project/ACME-2026-001/
---

# Customer Onboarding Acceleration

## Goal

Cut time-to-first-value for new B2B customers from 14 days to under 3 days by 2026-Q4.

## Scope

### In scope

- Self-service signup flow
- Salesforce CRM integration
- HubSpot lifecycle sync

### Out of scope

- Mobile app onboarding
- Free-tier conversion

## Constraints

- **Budget:** USD 120k engineering, USD 30k tooling
- **Deadline:** 2026-09-30 (end of FY26 Q3)
- **Regulatory:** GDPR, SOC2
- **Personnel:** 2 FTE eng, 0.5 FTE design; depends on platform team for SSO
- **Technical:** must reuse existing identity provider; cannot fork the auth stack

## Success criteria

- Median onboarding time for new B2B customers ≤ 3 days (P50)
- 90 % of new accounts active within 7 days
- Zero regressions in existing self-service signup conversion rate
```

## References

- PM agent preflight (enforcement): [`agents/pm.md`](../../agents/pm.md)
- Project initiation workflow: [`workflows/project-initiation.md`](../../workflows/project-initiation.md)
- Per-project directory convention: see [`CLAUDE.md`](../../CLAUDE.md) → *Per-project artifact layout*
- Origin specification: `spec-kit-pm-playground/docs/issues/internal/001-project-initiation-gate.md`
