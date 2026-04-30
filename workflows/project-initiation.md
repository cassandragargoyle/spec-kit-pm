# Workflow: Project Initiation

The **Initiation gate** runs **once per project**, at the start, before any planning artifact (Gantt chart, risk register, KPI sheet, decision log entry, status report) is produced. It establishes who authorised the project, who owns it, and where its artifacts live.

This workflow precedes the iterative loop:

```text
[Initiation gate]  →  Spec  →  AI Plan  →  Execution  →  Validation  →  Update Spec
                       ▲                                                    │
                       └────────────────────────────────────────────────────┘
```

The Initiation gate is enforced mechanically by the [PM agent preflight](../agents/pm.md): if `<artifact_directory>/project.md` does not exist, has `status` other than `active`, or does not name exactly one Project Manager with email, the agent MUST refuse to produce planning artifacts and instead produce a Charter draft.

## Steps

1. **Identify source authority.** Locate the contract, mandate, or formal decision that establishes the project. Capture the reference verbatim — it goes into the Charter's `source_authority` field.
2. **Allocate a Project ID.** Per the adopting org's naming rule (default suggestion: `<ORG>-<YYYY>-<NNN>` or contract-derived). The ID MUST be stable and unique within the org.
3. **Draft the Charter.** Copy [`templates/project/charter.md`](../templates/project/charter.md) to `specs/project/<project-id>/project.md`. Fill mandatory fields. Set `status: draft`.
4. **Assign a single named Project Manager.** Exactly one person with an email. OPTIONALLY assign a Deputy for unavailability cover (not a co-owner).
5. **Sponsor sign-off.** The Sponsor reviews the Charter. On approval, change `status` to `active` and bump `updated`. Commit.
6. **Create the artifact directory.** `specs/project/<project-id>/` with `project.md` (the Charter) committed.
7. **Initiation gate satisfied.** From this point the iterative loop may begin: `/specpm.spec`, `/specpm.plan`, `/specpm.risks`, `/specpm.review`, `/specpm.report`.

## Inputs

- Source authority document (contract, mandate, board minutes, etc.)
- Adopting org's Project ID rule (from the org profile)
- Named Project Manager and Sponsor

## Outputs

- `specs/project/<project-id>/project.md` (the Charter, `status: active`)
- `specs/project/<project-id>/` directory ready for iterative artifacts

## Failure Modes & Agent Behaviour

| Missing input | Agent behaviour |
| --- | --- |
| No source authority | Refuse to set `status: active`. Ask for the reference. |
| No Project ID rule | Use the default suggestion; flag for the org to confirm. |
| No named Project Manager | Refuse to set `status: active`. Ask for one named person with email. |
| Multiple Project Managers proposed | Refuse. Ask which one is the PM and (optionally) which is the Deputy. |
| Sponsor not identifiable | Refuse to set `status: active`. Ask. |

The agent never silently invents any of these.

## References

- Charter template: [`templates/project/charter.md`](../templates/project/charter.md)
- PM agent preflight: [`agents/pm.md`](../agents/pm.md)
- Origin specification: `spec-kit-pm-playground/docs/issues/internal/001-project-initiation-gate.md`
