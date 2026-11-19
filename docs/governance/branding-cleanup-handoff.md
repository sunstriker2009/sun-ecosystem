# Handoff for the SUN branding cleanup

The owner chose to keep Ecosystem and Foundry separate. Ecosystem owns the shared policy and registry. Foundry owns the factory, installer, and operational documentation. The goal is a consistent imagery package with minimal historical baggage. See the [audit and per-repository checklists](branding-cleanup-audit.md) for the requested layout, live dependencies, and repository baselines.

## Review decisions

- Confirm whether the SUN parent brand needs the full icon set.
- An incoming installer package may contain `preview.png`. Install it as `branding/assets/concept-artwork.png` when present. Review font and style preservation and rollback from existing numbered snapshots.
- Defer `asset-manifest.json` until its purpose and consumers are clear.
- Agree whether to retire Workbench’s unused-looking extra icon sizes and social exports after checking distribution outside Git.

## Suggested rollout for review

1. Agree on the package contract in Ecosystem and review the Foundry compatibility changes. Coordinate Foundry’s template seed checks with the planned Strata tree.
2. Stage any shared-action pin changes needed for the new format. Coordinate Ecosystem’s move from `branding/registry/` to top-level `gallery/` with the registry image paths, README generation, gallery validation, and Foundry workflows. Check installer, rollback, template provisioning, and gallery validation before removing dependent paths.
3. Propose focused cleanup PRs in the affected repositories. Keep product PRs and docs local in scope. Ecosystem and Foundry can reference multiple repositories when coordinating the rollout.
4. Use the approved layout for CodeFolio when its repository and branding are taken up.

## Starter message for the next thread

> Continue the SUN branding cleanup from the temporary Ecosystem draft PR, `docs/branding-cleanup-audit`. Read `docs/governance/branding-cleanup-audit.md` and this handoff. Verify GitHub main and any relevant open PRs before acting. Use the audit and checklist for review, and wait for my direction on which cleanup changes to implement. Keep Ecosystem and Foundry separate. Keep shared policy, active gallery assets, and supporting fonts and styles in scope when reviewing dependencies.

This draft holds review material only. No assets, automation, or published policy were changed.
