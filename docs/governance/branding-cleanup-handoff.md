# Handoff for the SUN branding cleanup

The owner chose to keep Ecosystem and Foundry separate. Ecosystem owns the shared policy and registry. Foundry owns the factory, installer, and operational documentation. The goal is a consistent imagery package with minimal historical baggage. See the [audit and per-repository checklists](branding-cleanup-audit.md) for the requested layout, live dependencies, and repository baselines.

## Review decisions

- Confirm whether the SUN parent brand needs the full icon set.
- Scope imagery installation to `branding/assets/`. Install incoming `preview.png` as `branding/assets/concept-artwork.png` when present and preserve supporting fonts and styles. Keep revision bookkeeping separate and review rollback from existing numbered snapshots.
- Maintain `branding/manifest.json` separately from imagery installation. It holds current product metadata such as `family-id`, `product-name`, and `short-description`. Defer the separate `asset-manifest.json` proposal.
- Use exactly 16, 24, 32, 48, 64, 128, 256, 512, and 1064 px for icons. Coordinate the switch from 1024 px with the generator, validator, and existing packages.
- Agree whether to retire Workbench’s unused-looking extra icon sizes and social exports after checking distribution outside Git.

## Suggested rollout for review

1. Agree on the package contract in Ecosystem and review the Foundry compatibility changes. Coordinate Foundry’s template seed checks with the planned Strata tree.
2. Stage any shared-action pin changes needed for the new format. Coordinate Ecosystem’s move from `branding/registry/` to top-level `gallery/` with the registry image paths, README generation, gallery validation, and Foundry workflows. Check installer write boundaries, rollback, template provisioning, and gallery validation before removing dependent paths.
3. Propose focused cleanup PRs in the affected repositories. Keep product PRs and docs local in scope. Ecosystem and Foundry can reference multiple repositories when coordinating the rollout.
4. Use the approved layout for CodeFolio when its repository and branding are taken up.

## Starter message for the next thread

> Continue the SUN branding cleanup from the temporary Ecosystem draft PR, `docs/branding-cleanup-audit`. Read `docs/governance/branding-cleanup-audit.md` and this handoff. Verify GitHub main and any relevant open PRs before acting. Use the audit and checklist for review, and wait for my direction on which cleanup changes to implement. Keep Ecosystem and Foundry separate. Keep shared policy, active gallery assets, and supporting fonts and styles in scope when reviewing dependencies.

This draft holds review material only. No assets, automation, or published policy were changed.
