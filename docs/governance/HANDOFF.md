# SUN governance handoff

Snapshot: 2026-11-15 (America/Toronto), before governance thread archival and memory cleanup. Reviewed main: `37e87da0901cc3ac913f79cfc77e0b0c82d5f05e`.

## Authority and entry points

This repository is the source of truth for names, permanent IDs, policy, registry and shared operator guidance. Implementation details belong in their owning repositories. Start with [product registry](../../registry/PRODUCTS.md), [infrastructure registry](../../registry/INFRASTRUCTURE.md), [Git policy](GIT-WORKFLOW.md), [branding standard](PRODUCT-BRANDING.md), [workflow handbook](../workflows/README.md), and [reusable thread handoff](../prompts/thread-handoff.md).

| Repository | Responsibility | Resume note |
| --- | --- | --- |
| sun-ecosystem | SUN-G001; governance, identity registry, gallery, handbook | This note |
| sun-strata | SUN-G002; stack-agnostic template | [STRATA handoff](https://github.com/sunstriker2009/sun-strata/blob/main/docs/GOVERNANCE-HANDOFF.md) |
| sun-foundry | SUN-G003; provisioning, governance tools and shared branding automation | [FOUNDRY handoff](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/GOVERNANCE-HANDOFF.md) |

## Decisions to preserve after memory cleanup

- Confirmed products are OUTPOST (SUN-001, `Sun.Security`) and WORKBENCH (SUN-002, `Sun.Workspace`). HALO is superseded by OUTPOST. WORKBENCH's earlier SUN-009 assignment was explicitly corrected to SUN-002.
- Products use SUN-NNN; established governance/infrastructure uses SUN-GNNN. IDs are sequential upon confirmation, permanent, never reserved for proposals or reused. Current next IDs are SUN-003 and SUN-G004; read the live registry before assignment.
- ORBIT/NOVA/PRISM/PULSAR/LUMEN/BEACON/FORGE remain unnumbered proposals. MarketPilot AI is an independent application and intended OUTPOST integration target, not a registered SUN product.
- Internal approval does not establish trademark/domain/package clearance. Do not infer a new identity from artwork or export filenames. The owner has explicitly approved WORKBENCH and sun-workbench; Gatehouse identity reconciliation remains outside this change.
- Approved original artwork is canonical. Preserve PNG consistency across banners, symbols and icons. Vectors are optional adaptations when useful; never replace approved raster artwork with a visually similar regeneration.
- Main is protected and PR-only; required checks, applicable human security review, resolved conversations and squash-only merges apply. Keep GitHub as the system of record.

## Current shared automation status

The operator reported the final five-repository governance alignment/audit successful. This review read repository state and merged PRs; it did not run a fresh live settings audit. The ecosystem's universal `gallery` check was merged in [#28](https://github.com/sunstriker2009/sun-ecosystem/pull/28). Preserve its execution on every PR, including documentation changes.

FOUNDRY's reversible installer and same-branch hook are merged ([#62](https://github.com/sunstriker2009/sun-foundry/pull/62), [#63](https://github.com/sunstriker2009/sun-foundry/pull/63)); ecosystem guidance merged in [#29](https://github.com/sunstriker2009/sun-ecosystem/pull/29) and [#30](https://github.com/sunstriker2009/sun-ecosystem/pull/30). WORKBENCH [#39](https://github.com/sunstriker2009/sun-workbench/pull/39) merged the first real installation; its main contains v1/v2 snapshots and current.json. Live rollback and broader opt-in remain pending. Foundry, STRATA and ecosystem have no same-branch hook in the reviewed trees.

Numbered ZIPs live at `branding/revisions/vN.zip`: v1 backs up existing assets, v2 onward capture installed state, and rollback creates a new version. Legacy archives have not been removed. Merging a product branding PR approves its canonical `branding/assets/symbol.png` for existing daily/manual gallery reconciliation. Digests detect changes; they do not substitute for visual approval. The historical symbol approval ledger is not a current additional approval gate.

## Resume priorities and boundaries

1. Re-read the three handoffs and current main/open PRs/runs; check whether paired documentation PRs have merged before treating new text as authoritative.
2. If authorized, validate rollback on one selected adopter, then consider explicit per-repository hook adoption and a separate archive migration.
3. Reconcile any approved new public identities with registry and recorded decisions only after confirming owner direction; do not guess from asset names.
4. Update the central handbook alongside workflow changes. Keep product implementation/milestones in product repos; WORKBENCH's [paused-work handoff PR #40](https://github.com/sunstriker2009/sun-workbench/pull/40) must remain respected.

No new schedules, administrative changes, branding rollout, product implementation, memory edits or thread archival were performed by this documentation task. Existing daily symbol reconciliation remains separate from manual governance audit/alignment. Prefer low-frequency/path-filtered auxiliary checks without making required checks disappear on documentation PRs.

## Resume rules

Read current repository documentation and live GitHub state before acting; this snapshot is not a standing authorization to resume implementation or administrative changes. Preserve explicit pauses. Use feature branches and PRs, required checks, applicable human review and squash merges; never push directly to protected main or weaken protection to make a verifier pass. Batch related fixes, avoid duplicate CI and unnecessary reruns, and stay within the owner's free GitHub Actions budget. Never store tokens in documentation.

Before continuing, inspect open PRs, branch tips and latest workflow results. Distinguish implementation, operator-reported live validation and independently verified evidence. Re-run read-only checks when needed; do not infer current compliance from an old green report. Do not create disposable repositories, change settings, roll out hooks, migrate archives or resume paused product work just because it appears in a next-step list.

## Owner-approved product rename

The owner approved ASTELVO → WORKBENCH by Sun and repository `sunstriker2009/sun-workbench`. This supersedes earlier notes treating Workbench naming as unverified. SUN-002 and `Sun.Workspace` stay unchanged. The historical ASTELVO Development schedule and product feature development remain paused. See [naming decision](https://github.com/sunstriker2009/sun-ecosystem/blob/main/decisions/0004-workbench-rename.md).
