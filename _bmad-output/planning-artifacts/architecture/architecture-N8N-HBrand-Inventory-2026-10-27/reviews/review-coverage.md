# Independent coverage and builder review

Reviewed and rechecked: 2026-10-27. Scope: the discussion-derived specification kernel and four local companions, decision/discussion records, architecture spine, PRD, DESIGN, EXPERIENCE, and the preserved bilingual example. Recheck additionally covered the new epic backlog, requirement-coverage map, roadmap and implementation-readiness assessment. This review assesses the documentation baseline, not product execution or live-release readiness. Operational/index files still being authored were excluded from missing-link findings.

## Verdict

**PASS ON RECHECK.** The substantive owner requirements are preserved and open business inputs are explicitly retained. The original medium contract-self-containment finding COV-1 is resolved: exact integration locations are now in a mandatory companion and the decision/question register is adopted. No high-severity source omission, invented model winner, falsely claimed implementation, or additional unanswered business decision was found in this coverage pass.

## Finding COV-1 — Exact integration locations sit outside the declared complete contract

- Status: **resolved on recheck**; original finding and reasoning are preserved below.
- Severity: medium.
- Evidence at review time: `SPEC.md:6-15` lists the mandatory companions, while `SPEC.md:70` says only “specified Drive folder”; `requirements.md:50` similarly says “owner-specified folder.” Neither the kernel nor those listed companions contains the exact Drive folder URL or `https://inventorysuite.neurix.uk/products/new`. The locations are correctly retained in the root README and `docs/source-evidence.md`, but those files are outside the declared complete contract.
- Impact: a downstream consumer loading only SPEC and its listed companions cannot recover the exact source or destination without consulting additional organizational/context documents. A builder would need to discover which locations “specified” refers to even though the owner supplied them.
- Correction: put both exact URLs in the source/target-scope section of `requirements.md`. Include the decision/question register as an adopted companion, or fully carry its load-bearing authority and question details in the mandatory package, because SPEC delegates full question wording, owners and blocking effects to that register.
- This is a contract self-containment correction, not a missing-user-information request. No further user answer is needed.
- Recheck evidence: `SPEC.md` now lists `../../../docs/decisions-and-open-questions.md` under `companions`; the Source and target scope section of `requirements.md` contains the exact Drive folder URL, `https://inventorysuite.neurix.uk/products/new`, and حفظ المنتج. The complete declared contract can now recover the integration locations and full question authority.

## Preserved source requirements

| Owner requirement | Preserved in contract |
| --- | --- |
| Local n8n coordinates the whole process | CAP-12; FR-23/FR-24; AD-1/AD-9. |
| Import the intended Drive Excel workbooks and worksheets | CAP-1; FR-1/FR-2; AC-1/AC-2. Exact URL placement was COV-1 and is resolved. |
| One barcode per source row; investigate duplicates/existing records first | CAP-2; FR-3/FR-4; duplicate outcomes; AC-3 through AC-5. |
| Do not silently infer stock addition or replacement | Constraints; duplicate outcomes; Q-06/Q-14; AC-4. |
| One stable parent SKU per confirmed design across colours and sizes | CAP-3; FR-5/FR-6; identity contract; AC-6/AC-8. |
| Use original images with barcode similarity/adjacency as clues, preserving distinct designs | FR-6; content/imagery evidence rules; AC-7; AD-2/AD-3. |
| Separate product/size attributes while preserving source values | CAP-4; FR-7/FR-8; canonical fields; AC-9/AC-10. |
| Improved English and Arabic titles and complete descriptions | CAP-5; FR-9/FR-10; content companion; preserved owner example; AC-11/AC-12. |
| Photorealistic appropriate human model, front/back/sides and colour-family consistency | CAP-7; FR-13/FR-14; content/gallery contract; AC-14. |
| Browser-based Gemini/ChatGPT comparison and owner review of first generated images | CAP-6/CAP-8; FR-11/FR-12 and FR-15/FR-16; AC-13/AC-15. |
| Append generated/required fields to the same Drive workbook | CAP-9; FR-17/FR-18; proposed appended-column contract; AC-16/AC-17. |
| Owner login, actual inventory browser entry and Save | CAP-10/CAP-11; FR-19 through FR-22; UJ-2; AC-18 through AC-20. Exact URL placement was COV-1 and is resolved. |
| Saudi riyal currency, with selling-price meaning still unanswered | SAR constraints and canonical values; Q-01; AC-10/AC-18; AD-10. |

## Authority and consistency checks

- Confirmed decisions are distinguished from Docker/SQLite/worker, gallery reuse, Drive-link layout, review surfaces and rollout proposals.
- Price meaning, physical facts, real target controls, warehouse/taxonomy, complete lookup and write-back concurrency remain explicit blockers for their live paths. These are unresolved product inputs, not defects in documenting the discussion.
- Screenshot observations are not promoted into a verified integration schema, and the visible warehouse is not declared the owner's selection.
- Provider documentation is not reported as a measured Gemini/ChatGPT winner or proof of account availability.
- The user-provided writing example is preserved as a structural reference rather than defaults for other garments.
- Source variants, family identity, parent SKU and target identifiers remain distinct. Only observed colour/size pairs are created.
- Draft states and verification scenarios are not reported as installed software, executed acceptance tests or saved inventory records.
- The recovery rules distinguish uncertain Save outcomes from safely retryable pre-submission failures.

## Builder check

No additional owner decision beyond Q-01 through Q-15 is required merely to finish this documentation baseline. The listed questions intentionally prevent live implementation paths from guessing. Concrete transport, schema, versions and browser library choices are explicitly left to implementation under the shared semantics; they are not undocumented business requirements.

With COV-1 resolved, the package is sufficient to scope discovery/offline stories while retaining the recorded live-operation blockers. This verdict does not authorize declaring the entire application implementation-ready.

## Backlog and traceability recheck

A deterministic identifier comparison on the current files found 13 capability definitions, 26 functional requirements, 22 acceptance scenarios and 21 unique story definitions. Every CAP/FR/AC definition is present in the coverage map; every mapped story exists; each FR has an explicit story requirement reference; and the mapped FR/AC ownership agrees with its defined capability. No missing mappings, duplicate story IDs or ownership mismatches were found.

Semantic spot checks confirm that the backlog retains all stories as backlog, the roadmap is proposed rather than scheduled, and the readiness assessment explicitly fails overall live-import readiness. In particular, SAR is retained without resolving Q-01, existing-stock updates remain blocked by Q-06/Q-14, and target mapping/lookup, write-back concurrency and later image acceptance remain evidence-dependent. Coverage is documentation coverage, not an executed test result or implementation completion claim.
