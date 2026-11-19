# Handoff for the SUN branding cleanup

The owner chose to keep Ecosystem and Foundry separate. Ecosystem owns the shared policy and registry. Foundry owns the factory, installer, and operational documentation. The goal is a consistent imagery package with minimal historical baggage. See the [audit and per-repository checklists](branding-cleanup-audit.md) for the requested layout, live dependencies, and repository baselines.

## Package decisions and review items

- The SUN parent brand has an optional full icon set. Temporarily fill missing size filenames with renamed copies of the closest available approved SUN icons. These parent-brand placeholders retain their original pixel dimensions.
- Scope imagery installation to `branding/assets/`. Install incoming `preview.png` as `branding/assets/concept-artwork.png` when present and preserve supporting fonts and styles. Keep revision bookkeeping separate and review rollback from existing numbered snapshots.
- Maintain `branding/manifest.json` separately from imagery installation. It holds current product metadata such as `family-id`, `product-name`, and `short-description`. Defer the separate `asset-manifest.json` proposal.
- Use exactly 16, 24, 32, 48, 64, 128, 256, 512, and 1024 px for product package icons.
- Agree whether to retire Workbench’s unused-looking extra icon sizes and social exports after checking distribution outside Git.

## Suggested rollout for review

1. Agree on the package contract in Ecosystem and review the Foundry compatibility changes. Coordinate Foundry’s template seed checks with the planned Strata tree.
2. Stage any shared-action pin changes needed for the new format. Coordinate Ecosystem’s move from `branding/registry/` to top-level `gallery/` with the registry image paths, README generation, gallery validation, and Foundry workflows. Check installer write boundaries, rollback, template provisioning, and gallery validation before moving items out of active paths.
3. Start each affected repository’s cleanup by creating `branding/recycling/`. Move approved removals there after updating live references. Preserve original paths inside the folder for recovery and exclude it from imagery installation and active branding checks. Keep product PRs and docs local in scope.
4. Use the approved layout for CodeFolio when its repository and branding are taken up.
5. Delete the recycling folders in a separate cleanup pass after validating the migration across all affected repositories.

## Starter message for the next thread

> Continue the SUN branding cleanup from the temporary Ecosystem draft PR, `docs/branding-cleanup-audit`. Read `docs/governance/branding-cleanup-audit.md` and this handoff. Verify GitHub main and any relevant open PRs before acting. Use the audit and checklist for review, and wait for my direction on which cleanup changes to implement. Keep Ecosystem and Foundry separate. Keep shared policy, active gallery assets, and supporting fonts and styles in scope when reviewing dependencies.

This draft holds review material only. No assets, automation, or published policy were changed.
