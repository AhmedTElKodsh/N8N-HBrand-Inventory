# Operations runbook

Baseline: 2026-10-27. This is the intended operating procedure for the future implementation. The runtime and workflow commands are not yet available; no installation or live operation is claimed. Use the [readiness assessment](../_bmad-output/planning-artifacts/implementation-readiness.md) before executing a live path.

## Prepare the environment

1. Verify the actual host, available disk/memory, Docker/native choices and browser support; select and pin the runtime under Q-12. Local n8n is required; its installation method is not selected.
2. Configure persistent n8n data and the chosen durable worker/identity state. Keep credentials, browser profiles, downloaded source workbooks, backups and generated assets outside Git.
3. Configure the deployed engine's own Drive connection and owner-authenticated image/inventory browser sessions. A connector available in this chat does not configure the local engine.
4. Retain recovery material for workflow configuration, job/identity state, source backups and n8n's required persistent configuration/key material. Select retention/recovery objectives under Q-13; no target is implied here.
5. Keep the host running and connected for Drive and provider/inventory access. Schedules, unattended startup and batch budgets require explicit configuration and measured limits.

## Start a bounded run

1. Select the source scope and freeze a versioned file/tab manifest. Record exclusions explicitly.
2. Complete the source-barcode index before clearing any row for enrichment. A partial/unreadable scope does not establish uniqueness. Link previous observations/imports and inspect actual inventory matches.
3. Investigate each missing/repeated/conflicting barcode first. Do not sum repeated quantities, change source barcodes, or update existing stock/price under an unspecified policy.
4. Establish family membership from original garment evidence. Preserve observed colour/size variants and their original values.
5. Complete supported facts and expose blockers. Confirm SAR price semantics, real required weight/dimensions, taxonomy and warehouse before the corresponding live action.

## Content and imagery

1. Produce English/Arabic titles and full descriptions from the same original-source fact record.
2. For the first comparison, use the same references and equivalent instructions in both provider websites. Record the displayed models, all attempts, downloads and corrections.
3. Show the originals beside the first outputs and wait for the owner's verdict. Apply corrections to a new revision, retaining rejected assets.
4. Bind acceptance to supplier-fact/image, family, content and asset revisions. A later style policy must be recorded separately; an unanswered review is pending.

## Enrich the source workbook

1. Preserve the original source revision and validate the prepared copy, including media/drawings/anchors and row alignment.
2. Establish conditional write support or an enforced exclusive editing window. A precheck-only read cannot protect an intervening edit.
3. Update the same Drive file, then read it back and verify both preservation and enriched values.
4. Track physical file revision separately from supplier facts and original image associations. Own enrichment must not produce endless reruns or invalidate unchanged acceptance, and genuine supplier changes must still invalidate affected outputs.

## Enter and verify inventory

1. Use the actual recorded target mapping and revalidate the intended payload/source/existence evidence.
2. Establish target uniqueness/idempotency or an enforceable exclusive inventory-writing window covering lookup through confirmed outcome. A local lock does not exclude another human or external integration.
3. Fill the form with the exact observed variants and accepted assets. Read back prepared controls before submission.
4. Persist SUBMITTING, intended payload identity and the durable reservation before clicking حفظ المنتج.
5. Reopen through fresh navigation and verify target identity, copy, SKU where supported, barcodes, colour/size membership, prices, quantities, warehouse and gallery. Record IMPORTED only when those checks establish the result.

## Recover common interruptions

| Condition | Safe response |
| --- | --- |
| Login expired | Pause the affected job; owner signs in through the real website; resume after verifying the current job/versions. |
| Missing weight or ambiguous price | Retain BLOCKED_FACTS and request the actual fact/meaning; do not substitute a zero or guessed selling price. |
| Same barcode in another file | Inspect exact source and target records; hold all affected observations until a documented resolution. |
| Different design hidden behind the same text | Keep separate families and show original garment evidence. |
| Provider failed before generation | Retry only within the selected budget and record the attempt; do not claim an absent download is an asset. |
| Source changed or was sorted | Revalidate current original values, semantic revision and row/image alignment; regenerate/review only the affected outputs. |
| Drive write outcome uncertain | Inspect the same file ID and revisions before another upload; preserve human edits. |
| Save may have reached inventory | Retain SUBMITTING/IMPORT_UNKNOWN and reservations, fence stale workers, and reconcile target-side evidence. A negative lookup alone does not rule out delayed commit or justify another Save. |
| Worker or n8n restarted | Load durable operation/review state. Do not release an uncertain reservation merely because a process died or timed out. |

## Rollback and maintenance

A workbook backup can restore source content after a reconciled failed update; it does not undo an inventory product or opening-stock event. Inventory corrections/deletion follow an explicit owner-selected policy and actual target capabilities. Snapshot/restore procedures must preserve identity, approvals and outstanding submission reservations together. Upgrades require checking the selected runtime's current official guidance and rerunning the affected acceptance scenarios; this runbook contains no copied obsolete n8n launch command.

Record operations with timestamps, source/target identifiers, revisions, issue codes, evidence and outcomes. Exclude passwords, tokens, cookies and reusable account state. Keep pilot results separate from wider release evidence.
