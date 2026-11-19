# SUN branding package cleanup audit

**Status:** Temporary review material. The current branding standard stays in effect until a separate policy change is approved.  
**GitHub snapshot:** 2026-11-19. See [audited commits](#audited-commits) for reproducible baselines.

## Proposed layout

    branding/
      assets/
        icons/
          icon-{size}.png
        readme-banner.png
        symbol.png
        concept-artwork.png
        … supporting font and style files
      revisions/
      manifest.json

- Only `branding/assets/` represents the installable imagery package. Imagery installation writes only within that directory and preserves supporting files there. Files and directories elsewhere under `branding/`, including `manifest.json` and `revisions/`, are outside the installer’s write scope.
- Required imagery consists of the README banner, canonical symbol, and square PNG icons at exactly **16, 24, 32, 48, 64, 128, 256, 512, and 1064 px**. Update the generator and validator from the audited 1024 px requirement to 1064 px.
- Optional `branding/assets/concept-artwork.png` is the agreed artwork reference used to build the asset package. An incoming installer package may contain `preview.png`. During installation, rename it to `concept-artwork.png` at the installed path.
- Keep supporting fonts, font licenses, styles, and design tokens used by the repository.
- Drop repository-specific branding guides and README files inside branding, along with archive folders, reference folders, and historical review material. Keep root README banners and links to active assets. Ecosystem-wide brand and naming policy still has a purpose.
- `branding/manifest.json` holds metadata for the current product, including `family-id`, `product-name`, and `short-description`. Provision or maintain it separately from imagery installation. Defer the separate `asset-manifest.json` proposal.
- Keep existing numbered ZIP snapshots in `revisions/`. Handle snapshot creation and revision bookkeeping separately from imagery installation. Confirm how rollback will read older snapshots and restore assets within `branding/assets/`.

## Ecosystem

Add a top-level `gallery/` directory alongside `branding/` to replace `branding/registry/` as the home of the Ecosystem gallery images.

Findings: The parent brand guide, concept page, reference SVGs and exploratory artwork overlap the retained branding policy or record historical work. The archived banner and symbol are byte-identical to their active copies. The old sun-oryva gallery image is an unreferenced, byte-identical copy of the current Outpost gallery image. Four current gallery images are live outputs consumed by the generated README and validator. The parent brand has an active banner and symbol and lacks the standard icon set.

- [ ] Revise the Product Repository Branding Standard for stable paths and the streamlined package. Remove requirements for per-repository guides, archive copies, and reference folders. Keep shared visual and naming policy.
- [ ] Fold any still-current guidance from the parent brand guide or visual identity notes into shared policy. Remove obsolete artwork documentation and fix links.
- [ ] Move the four active gallery images from `branding/registry/` to `gallery/` and remove the unused old gallery image. Update the icon paths in `registry/repositories.json`, the README gallery generator and validator, and Foundry workflows and scripts that publish or reconcile gallery images. Coordinate the path switch before retiring `branding/registry/`.
- [ ] Remove `branding/archive` and `branding/assets/refs` after checking live references.
- [ ] Confirm whether the SUN parent brand itself must ship the full icon set. If it does, add the icons from the approved SUN source.
- [ ] Run gallery validation and check the active README, policy, and registry links.
- [ ] Apply the product metadata manifest separately from imagery installation in the repositories covered by the approved package contract.

[Branding tree](https://github.com/sunstriker2009/sun-ecosystem/tree/main/branding) · [Gallery catalog](https://github.com/sunstriker2009/sun-ecosystem/blob/main/registry/repositories.json) · [Branding standard](https://github.com/sunstriker2009/sun-ecosystem/blob/main/docs/governance/PRODUCT-BRANDING.md)

## Foundry

Findings: Foundry has the core imagery. The guide, adoption checklist, reviews, archive, and references contain old comparisons, vectors, a superseded icon set, and a manifest buried in refs. The live asset configuration and CI use the archived banner path. The installer accepts legacy social and reference PNGs, ignores the export-root PREVIEW.png and manifest.json, and rejects `branding/assets/concept-artwork.png` today. It replaces icons and preserves other existing non-icon assets on install. Numbered snapshots capture assets, and rollback restores those files. The Strata seed logic checks exact template branding paths and hashes and writes a replacement brand guide.

- [ ] Align the generator, installer, validators, and package documentation with the new layout and exact icon sizes. Install an incoming `preview.png` as optional `branding/assets/concept-artwork.png`. Limit installer writes to `branding/assets/` and preserve supporting fonts and styles there. Account for legacy packages and snapshots that contain a 1024 px icon during rollout and rollback.
- [ ] Keep `branding/manifest.json` and revision bookkeeping outside imagery installation. Define how product metadata is maintained during provisioning and verify that installing imagery leaves the manifest and revision files untouched.
- [ ] Repoint the active generator config and CI from the archived banner to the approved source. Validate output before deleting the old copy.
- [ ] Update the factory seed fingerprint, generated README and checklist, and resume/verification paths that expect a brand guide. Test provisioning against the planned Strata tree and recovery of any supported older seed state.
- [ ] Remove obsolete branding guides, archive, references, and review artifacts after their active dependencies are resolved. Keep operational instructions and live generator configuration.
- [ ] Run installer, rollback, asset generation, and factory seed/recovery checks. Identify workflows that pin the shared action and stage compatible pin updates before they receive the new package format.

[Branding tree](https://github.com/sunstriker2009/sun-foundry/tree/main/branding) · [Installer](https://github.com/sunstriker2009/sun-foundry/blob/main/scripts/install-branding.py) · [Seed script](https://github.com/sunstriker2009/sun-foundry/blob/main/scripts/prepare-product-branding.sh)

## Strata

Findings: Strata has the required imagery. Its archived banner duplicates the active banner byte-for-byte. The brand guide, archive, and four reference SVGs are redundant. Foundry’s seed fingerprint has a specific dependency on Strata’s current assets and guides.

- [ ] Coordinate the template tree change with Foundry’s seed support before merging.
- [ ] Remove the brand guide, archive, and references. Fix template, setup, and asset preparation instructions that expect those paths.
- [ ] Retain the active banner, symbol, and revision directory scaffold. Update the icon set to the proposed sizes and coordinate product metadata provisioning with Foundry.
- [ ] Verify template CI and the coordinated seed path can remove template branding safely and produce a neutral repository without a brand guide.

[Branding tree](https://github.com/sunstriker2009/sun-strata/tree/main/branding) · [Template guide](https://github.com/sunstriker2009/sun-strata/blob/main/docs/TEMPLATE-GUIDE.md)

## Foundry Pilot

Findings: The generated brand guide is the only current file under branding. The root README and setup checklist refer to it. No artwork package is installed.

- [ ] Remove the scaffold guide and fix references in the README and setup checklist.
- [ ] Verify the repository remains a usable pilot with no fabricated artwork or package files. Use an approved package only if an installer validation run is separately authorized.

[Branding tree](https://github.com/sunstriker2009/sun-foundry-pilot/tree/main/branding) · [Setup checklist](https://github.com/sunstriker2009/sun-foundry-pilot/blob/main/docs/REPOSITORY-SETUP.md)

## Workbench

Findings: Workbench has the required imagery. Its guide, compatibility pointer, archive, references, and retired vector build artifacts are extra. The existing manifest predates the active W2 assets and names removed files and old source paths. The 96, 180, and 192 px icons and two social PNGs had no checked-in consumer in the audit. The build reads icon-512.png. The branding directory also has CSS/JSON design tokens and a font license.

- [ ] Remove obsolete guides and pointers, archive and references, and update README and developer links. Review the old build wrapper before deleting its referenced archive.
- [ ] Replace the 1024 px icon with a 1064 px icon from the approved artwork. Check external distribution consumers before removing other icon sizes or social PNGs. Keep the required 512 px build source.
- [ ] Preserve tokens.css, tokens.json, the font license, and revision snapshots. Verify the app build and any packaging-time native icon generation.

[Branding tree](https://github.com/sunstriker2009/sun-workbench/tree/main/branding) · [Build script](https://github.com/sunstriker2009/sun-workbench/blob/main/tools/build.mjs)

## Outpost

Findings: Outpost has the required imagery. Its guides, compatibility pointer, v2 handoff, archive, and refs are extra. The canonical symbol, 1024 px icon, and versioned reference PNG are byte-identical. Preserve the canonical symbol at its active path. Update the icon set to use 1064 px in place of 1024 px. The archived v2 banner differs from the active banner even though the guide calls it an exact copy.
- [ ] Remove the redundant reference PNG, guides, handoff, and archive. Remove or replace old README links.
- [ ] Keep approved active artwork and any package documentation that explains a live workflow. Verify the active symbol path still works for the gallery.

[Branding tree](https://github.com/sunstriker2009/sun-outpost/tree/main/branding) · [Branding ZIP workflow guide](https://github.com/sunstriker2009/sun-outpost/blob/main/docs/BRANDING-ZIP-INSTALLER.md)

## CodeFolio and MarketPilot AI

- [ ] Apply the approved package contract to CodeFolio. Maintain its product metadata at provisioning and install the imagery under `branding/assets/`. No CodeFolio repository was visible at the audit checkpoint, so there is no existing tree to trim.
- [ ] Treat MarketPilot AI as independent. Its main branch has no branding directory, so there is no branding cleanup to plan there.

## Audited commits

| Repository | GitHub main at audit |
|---|---|
| sun-ecosystem | [05e816a2f578](https://github.com/sunstriker2009/sun-ecosystem/commit/05e816a2f578350d69cae3ea35a23e0775ad948f) |
| sun-foundry | [50848c37c7d1](https://github.com/sunstriker2009/sun-foundry/commit/50848c37c7d171da35e08f59e3b272a0db342616) |
| sun-strata | [23d9753737f4](https://github.com/sunstriker2009/sun-strata/commit/23d9753737f49bee29c465643b9eb85b47d4a5b3) |
| sun-foundry-pilot | [86fe57b36605](https://github.com/sunstriker2009/sun-foundry-pilot/commit/86fe57b36605700e36133a579aad53ee263553f8) |
| sun-workbench | [d95914f1d69f](https://github.com/sunstriker2009/sun-workbench/commit/d95914f1d69fb90711eb2a51b64329b86e4a029c) |
| sun-outpost | [39511c6b2ad1](https://github.com/sunstriker2009/sun-outpost/commit/39511c6b2ad1621f30b41888eaa9ad9be57cafcb) |
| sun-marketpilot-ai | [b47b202be4fa](https://github.com/sunstriker2009/sun-marketpilot-ai/commit/b47b202be4fa25560ce56ceb46d4ece91b7c7f30) |
