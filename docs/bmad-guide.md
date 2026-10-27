# BMad project guide and setup record

Setup date: 2026-10-27. The installed BMad `bmad` skill's supported `scripts/setup.py` command created this project's `_bmad` configuration and shared/module helper scripts. No classic installer cache or hand-made agent registry was substituted.

## Verified setup result

- BMad version reported by setup: **6.13.0-next**.
- Setup result: **created**; `current: true` for that setup/status snapshot.
- Modules: **core-tools** and **method**.
- Shared scripts, module scripts, `_bmad/config.toml` and the personal-override ignore file were created.
- Pending configuration questions, missing module records, unmet requirements and reported problems: none in the verified snapshot.
- This is BMad tooling state. It is not n8n installation, application readiness or live acceptance.

## Artifact configuration

`_bmad/config.toml` sets:

```toml
[core]
project_name = "N8N-HBrand-Inventory"
output_folder = "{project-root}/_bmad-output"

[modules.bmm]
planning_artifacts = "{project-root}/_bmad-output/planning-artifacts"
implementation_artifacts = "{project-root}/_bmad-output/implementation-artifacts"
project_knowledge = "{project-root}/docs"
```

The `bmm` configuration table is the supported helper's emitted configuration, not a manually invented module registry. Team overrides belong under `_bmad/custom/`; personal `*.user.toml` answers are ignored from Git.

## Entry points

Use the installed BMad skill names in the agent host; a standalone `bmad` shell executable is not assumed:

| Skill | Project use |
| --- | --- |
| `bmad` | Inspect setup/status or run the supported setup/repair path. |
| `bmad-spec` | Append resolved decisions, preserve CAP identifiers and re-derive the canonical spec and companions. |
| `bmad-party-mode` | Reopen a focused discussion; this session's final outcome is in its project memlog. |
| `bmad-prd`, `bmad-architecture`, `bmad-ux` | Refine the corresponding draft artifacts when new source decisions arrive. |
| `bmad-create-epics-and-stories` | Refine the backlog from the updated contract without inventing missing business decisions. |
| `bmad-sprint-planning` | Reassess readiness; generate sprint tracking only after the relevant scope passes the gate. |
| `bmad-build` | Carry an actually delegated implementation slice through implementation and verification. |

From the repository root, configuration can be inspected with:

```powershell
uv run _bmad/scripts/resolve_config.py --project-root .
```

To inspect/repair installation state, invoke the installed `bmad` skill's status/setup flow. Its setup writer lives in the installed skill and owns `_bmad/scripts`; do not edit the copied shared scripts to change product behaviour.

## Documentation derivation and status

- The spec folder contains an append-only `.memlog.md`; specification decisions and review corrections were written using `_bmad/scripts/memlog.py`.
- Brief, PRD, architecture, UX and party workspaces also retain their session memlogs.
- SPEC and authored companions are derived outputs. Record a new decision in the appropriate log before re-deriving through `bmad-spec`; retain stable IDs.
- The brief/PRD/spines remain `draft` because business and integration questions remain open. Creating a document does not grant owner approval to every proposed design choice.
- Independent architecture review reports are in the architecture workspace's `reviews/` directory. The final documentation check records resolved findings separately from current live readiness.
- No formal interactive wizard completion, invented `stepsCompleted` values, activated sprint or completed application story is claimed. The package was produced as a discussion-derived documentation pass, not as evidence that every interactive BMad ceremony was completed.

## Resume procedure

Read [project context](project-context.md), the [question register](decisions-and-open-questions.md), the SPEC and all its companions, and the latest relevant memlog. Confirm actual files/runtime/evidence before changing a status. Resolve Q-01 and inspect the authenticated target contract as the next focused discovery work; other independent offline tasks can be scoped separately.
