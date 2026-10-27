# Architecture contract review

Reviewed: 2026-10-27. Lens: adversarial consistency between independently implemented units. Initial verdict: **CONCERNS — four contract clarifications recommended**. This reviews the proposed documentation, not an application implementation. No live operation or software test was performed.

**Current recheck verdict: PASS for these four documentation corrections.** All initial findings below are preserved as the review history. The recheck section records how each was resolved. No new load-bearing inconsistency was found in the corrected scope. Implementation readiness remains governed by the open questions and required live evidence.

## Scope

Read `AGENTS.md`, the specification kernel and its four local companions, the decision/question register, the architecture spine, and UX `EXPERIENCE.md`. Existing business questions, deferred runtime choices and deliberately unimplemented controls are not counted as documentation defects. Temporary links to documents still being written were excluded.

## CON-1 — High: duplicate checking needs a source-scope completeness barrier

**References:** `requirements.md` FR-1/FR-3/FR-4; `data-contracts.md` identity and existence sections; spine AD-2.

**Divergent compliant units:** A bounded workbook worker enumerates all file IDs, then parses and releases each workbook in turn. A duplicate service checks every currently registered observation and inventory record before releasing a row for enrichment. Neither component has an explicit contract telling it that the source barcode index must cover every selected workbook revision before a row is cleared. A barcode first seen in workbook 1 can pass and be enriched/imported before the same barcode in workbook 99 is discovered. The eventual duplicate flag arrives after the required first investigation.

**Why it matters:** A complete file manifest is not a complete barcode index. Without a completion marker bound to the selected source revisions, independently built components disagree about the meaning of a successful duplicate check.

**Minimal clarification:** Define a versioned run/source scope and an explicit barcode-index-complete state. Before clearing rows for enrichment or creation, the identity authority must establish index completeness for that selected scope, or hold affected work. Expansion or supplier-revision changes invalidate the relevant clearance. This can still process each large workbook in bounded fashion; it does not require loading all files into memory.

**Acceptance addition:** Put a repeated barcode in the last workbook of a selected run. Verify that its first observation cannot clear enrichment/import before the whole selected barcode index is complete, and that a changed/new source revision invalidates stale clearance.

## CON-2 — High: negative lookup does not by itself reconcile a delayed save or stale worker

**References:** `data-contracts.md` ABSENT_VERIFIED, SUBMITTING, IMPORT_UNKNOWN and operation identity; spine AD-4/AD-7; acceptance AC-20/AC-21.

**Divergent compliant units:** The first browser worker pauses immediately before clicking Save, or its submitted request remains in flight. A recovery worker performs fresh, complete target lookup, sees no record yet, calls that explicit reconciliation, releases the reservation and retries. The original worker/request then completes. Both paths can satisfy the current “fresh navigation before another action” wording while producing two saves.

**Why it matters:** A durable local reservation and a negative search are necessary but do not establish that an earlier browser action can no longer take effect. Timeout alone is already excluded, but the definition of reconciliation still needs to exclude delayed effects.

**Minimal clarification:** A negative lookup cannot release an uncertain submission unless the prior attempt is established unable to produce a later effect, or verified target uniqueness/idempotency makes another attempt safe. Explicitly fence/revoke old worker authority and establish browser/request quiescence before retry authorization. If that cannot be proved for the actual site, retain IMPORT_UNKNOWN and require further evidence rather than declaring absence sufficient. Keep the same logical operation identity across recovery.

**Acceptance addition:** Delay server completion until after a recovery lookup and resume an old worker after recovery starts. The system must not authorize another effective Save from either path merely because a lookup was negative.

## CON-3 — High: local exclusivity does not close a race with other inventory writers

**References:** spine AD-2/AD-4/AD-7; `data-contracts.md` existence outcomes; requirements FR-21 and NFR-2.

**Divergent compliant units:** The proposed local mutation authority holds its family/variant reservation and the browser adapter rechecks absence immediately before creation. Another human or importer creates that variant on the inventory site between the lookup and Save. The local units obey every AD, but the site may accept a duplicate if its uniqueness behaviour is unverified.

**Why it matters:** Q-05 asks about complete lookup and Q-13 about concurrency limits; neither explicitly establishes a target-side uniqueness invariant or an exclusive window covering other writers. The contract currently promises repeat-safe creation more broadly than a purely local lock can guarantee.

**Minimal clarification:** Before the live pilot, verify server-enforced uniqueness for the relevant parent/variant identifiers, or establish and enforce an exclusive inventory-writing window for that scope. If neither is possible, document that safe automatic creation is blocked rather than claiming that a last-second search makes the operation atomic. This can be recorded as an implementation-discovery condition; it does not require choosing an API or solving it in this documentation pass.

**Acceptance addition:** Introduce an external create between the final existence check and the local Save. Verify a safe conflict/no-duplicate result under the established target uniqueness or exclusive-writing condition.

## CON-4 — Medium: distinguish workbook container revisions from supplier-fact revisions

**References:** `data-contracts.md` source workbook/row identity, write-back steps and review records; spine AD-5/AD-6; UX state patterns.

**Divergent compliant units:** The source adapter treats every Drive revision/content digest as a new source observation, including automation's appended columns. The approval service binds acceptance to the exact source revision and invalidates changes. After a correct write-back, it invalidates the just-approved gallery or creates a new row observation that no longer matches the approved payload. Another implementer may instead ignore every automation-labelled revision, without proving that supplier cells/images were unchanged. One loops or blocks; the other can preserve stale approval.

**Why it matters:** The contract already distinguishes self-triggering enrichment from supplier changes in intent, but it does not define the shared digest boundary and lineage that make that distinction reliable across units.

**Minimal clarification:** Keep a physical Drive/container revision for concurrency and preservation checks, and a separate supplier-content revision derived only from original supplier fields plus source image relationships/content. Record the enrichment revision lineage. Approval remains valid across a verified metadata-only enrichment only when supplier facts, family membership and source images are proven unchanged; genuine changes invalidate the affected acceptance.

**Acceptance addition:** Complete an automation-only enrichment and show that acceptance stays bound to unchanged supplier evidence, then alter an original cell or image and verify that the relevant acceptance is invalidated.

## No extra business decisions requested

These clarifications define shared safety/completeness semantics and can be recorded as proposed engineering constraints. They do not resolve price meaning, weight, target controls, supplier sizes, provider choice or later review policy on the owner's behalf. The existing register correctly leaves those questions open. The documentation also correctly distinguishes original product facts from generated images, parent SKU from variant barcodes, and planned behaviour from live evidence.

## Recheck — 2026-10-27

Re-read the current data contract and relevant CAP-2, FR-3/FR-16/FR-18/FR-21/FR-22, AC-4/AC-17/AC-20/AC-21, AD-2/AD-4/AD-6/AD-7, Q-05, and readiness R-3. Also checked that the four engineering-review correction entries are present in both the specification and architecture memlogs.

| Finding | Recheck disposition | Corrected contract evidence |
| --- | --- | --- |
| CON-1 | Resolved in documentation | Data-contract existence rules freeze the selected manifest and require its complete versioned barcode index before clearance, retain partial-scope uncertainty, and revalidate freshness. CAP-2, FR-3, AD-2 and AC-4 align, including a duplicate in the final workbook. |
| CON-2 | Resolved in documentation | Data-contract recovery rules explicitly fence stale workers and distinguish worker termination from cancellation of an in-flight server write. A negative lookup cannot release the reservation or authorize retry. FR-22, AD-7 and AC-20 require definitive outcome evidence or verified target guarantees. |
| CON-3 | Resolved in documentation | SUBMITTING prerequisites and the accompanying rule require verified relevant target uniqueness/idempotency or an enforced exclusive writing window; local reservations are explicitly insufficient. FR-21, AD-4, AC-21, Q-05 and readiness R-3 carry the condition. |
| CON-4 | Resolved in documentation | The identity contract separates physical workbook revision from supplier-content revision. Write-back recomputes original supplier values/image associations; reviews bind supplier-content/family facts, not enrichment-only physical revisions. FR-16/FR-18, AD-6 and AC-17 carry the distinction. |

**Outstanding findings from this review: none at the documentation-contract level.** The target's actual uniqueness behaviour, enforceability of an exclusive writing window, safe delayed-save reconciliation and source-preservation mechanisms still need implementation discovery and acceptance evidence. The revised documents correctly retain those as blocking conditions rather than claiming they have been demonstrated.

The current draft is internally consistent on the reviewed seams. This recheck is not an application test, live-target acceptance, or authorization to invent answers to the remaining business questions.
