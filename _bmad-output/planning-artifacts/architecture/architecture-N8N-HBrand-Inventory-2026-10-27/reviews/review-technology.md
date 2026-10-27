# Technology and reality review

Reviewed: 2026-10-27. Lens: BMad architecture gate, current technical claims and evidence boundaries.

**Verdict: PASS for the technical accuracy of the documentation baseline. No substantive technical corrections were found in the reviewed artifacts.** This verdict does not establish implementation readiness, account access, garment-generation quality, or a functioning integration.

## Scope

Reviewed the repository instructions, project context, source-evidence record, canonical specification, detailed requirements, data/content/acceptance companions, architecture spine, and UX documents. The review used the actual BMad setup state and current official references. Operational/index files were still being authored, so temporary missing links to those were excluded from this lens.

## Checked claims

| Area | Result | Evidence and limits |
| --- | --- | --- |
| Local n8n deployment | Supported as a proposed implementation route; not reported as installed. | The [current Compose guide](https://docs.n8n.io/deploy/host-n8n/install-options/install-using-docker-compose.md) documents local deployment and persistent storage. The specification leaves actual installation method and runtime pins under Q-12. |
| Outdated Docker instructions | Correctly identified and excluded from project configuration. | The [older Docker page](https://docs.n8n.io/deploy/host-n8n/install-options/install-with-docker.md) labels its content outdated and points to Compose. The source-evidence document also explicitly excludes the current guide's optional Assistant sandbox stack from selected project dependencies. |
| n8n waiting | Claimed within the documented mechanism's scope. | The [Wait-node documentation](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/) describes stored execution data and supported resume conditions. Project-level restart and repeat-safety remain acceptance scenarios, not accomplished results. |
| Gemini imagery | Capabilities are cited without an account-specific or quality guarantee. | [Google's current help page](https://support.google.com/gemini/answer/14286560?hl=en) describes reference edits, multiple references and character consistency. The package still requires the actual account/model comparison and owner review. |
| ChatGPT imagery | Reference editing and iteration are supported; website/API model equivalence is not assumed. | [Official OpenAI documentation](https://learn.chatgpt.com/docs/image-generation) describes reference-led edits, iterative corrections and account-dependent web availability. The package records the displayed website model during the future comparison instead of selecting one from an API catalogue. |
| Image-model selection | No measured winner is claimed. | CAP-6 and the content companion require comparable original inputs, retained attempts and the owner's recorded judgement. |
| Technical stack | Deferred choices stay proposals. | Docker/SQLite, worker library, transport and runtime versions are not falsely presented as owner-selected or installed. No arbitrary version pin is necessary to make this discussion-derived draft accurate. |
| Workbook updates | Safety is a future requirement, not an asserted provider guarantee. | The data contract requires an actually supported conditional write or enforced exclusive window and explicitly rejects a read-before-write check as a complete race solution. Q-09 blocks live write-back until the mechanism is established. |
| Inventory mapping and saves | Evidence boundary is preserved. | SKU/image controls, search coverage and save behaviour remain unverified until authenticated inspection. Fresh read-back and unknown-save reconciliation are specified acceptance obligations. |

## Repository reality checks

The supported BMad status command was run against this checkout. It reported `current: true`, version `6.13.0-next`, current shared and module scripts, current upstream module versions, no missing records, no pending configuration questions, no unmet requirements/recommendations, and no problems. This confirms the BMad tooling state at review time; it says nothing about n8n or the product integration.

The retained original children's-workbook inspection copy was independently re-read without modifying it. Its 947,211-byte size, worksheet `ورقة1`, 51 media files, and the recorded raw values for rows 26/28/47 match the source-evidence document. This checks the saved inspection artifact, not the current Drive revision or full folder.

## Preserved implementation gaps

Q-01 through Q-15 remain relevant. Provider/account access, browser reliability, target lookup completeness, actual inventory controls, source-write concurrency, required product facts and representative live acceptance must still be established. Their explicit deferral is appropriate for a documentation baseline and is not a claim that the system is ready to operate.
