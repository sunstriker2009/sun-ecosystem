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
        preview.png
        … supporting font and style files
      revisions/
      asset-manifest.json

- Required imagery consists of the README banner, canonical symbol, and PNG icons at **16, 24, 32, 48, 64, 128, 256, 512, and 1024 px**, matching the installer’s current required sizes.
- Optional **preview.png** represents the agreed artwork reference used to build the asset package. Use it only when the reference can be verified.
- Keep supporting fonts, font licenses, styles, and design tokens used by the repository.
- Drop repository-specific branding guides and README files inside branding, along with archive folders, reference folders, and historical review material. Keep root README banners and links to active assets. Ecosystem-wide brand and naming policy still has a purpose.
- Keep numbered ZIP snapshots in revisions. Decide how snapshot, rollback, and manifest behavior should work before changing the installer. Avoid editing existing snapshots during this cleanup.

## Ecosystem

Findings: The parent brand guide, concept page, reference SVGs and exploratory artwork overlap the retained branding policy or record historical work. The archived banner and symbol are byte-identical to their active copies. The old sun-oryva gallery image is an unreferenced, byte-identical copy of the current Outpost gallery image. Four current gallery images are live outputs consumed by the generated README and validator. The parent brand has an active banner and symbol and lacks the standard icon set and root manifest.

- [ ] Revise the Product Repository Branding Standard for stable paths and the streamlined package. Remove requirements for per-repository guides, archive copies, and reference folders. Keep shared visual and naming policy.
- [ ] Fold any still-current guidance from the parent brand guide or visual identity notes into shared policy. Remove obsolete artwork documentation and fix links.
- [ ] Remove branding/archive, branding/assets/refs, and the unused old gallery image. Retain the four active gallery images and their paths unless a separate gallery migration is approved.
- [ ] Confirm whether the SUN parent brand itself must ship the full icon set and manifest. If it does, add them from the approved SUN source.
- [ ] Run gallery validation and check the active README, policy, and registry links.

[Branding tree](https://github.com/sunstriker2009/sun-ecosystem/tree/main/branding) · [Gallery catalog](https://github.com/sunstriker2009/sun-ecosystem/blob/main/registry/repositories.json) · [Branding standard](https://github.com/sunstriker2009/sun-ecosystem/blob/main/docs/governance/PRODUCT-BRANDING.md)

## Foundry

Findings: Foundry has the core imagery. The guide, adoption checklist, reviews, archive, and references contain old comparisons, vectors, a superseded icon set, and a manifest buried in refs. The live asset configuration and CI use the archived banner path. The installer accepts legacy social and reference PNGs, ignores the export-root PREVIEW.png and manifest.json, and currently rejects the proposed preview and manifest paths inside branding. It replaces icons and preserves other existing non-icon assets on install. Numbered snapshots capture assets, and rollback restores those files. The Strata seed logic checks exact template branding paths and hashes and writes a replacement brand guide.

- [ ] Define the manifest schema and ownership. Decide whether Foundry generates it, validates one supplied by the package, or supports both. Use the root branding/asset-manifest.json path for the installed package.
- [ ] Align the generator, installer, and package documentation with the new layout. Cover optional assets/preview.png, preservation of fonts and styles, legacy package compatibility, and the behavior of older snapshots during rollback. Decide explicitly how revisions/current.json relates to the manifest.
- [ ] Repoint the active generator config and CI from the archived banner to the approved source. Validate output and add or refresh the root manifest before deleting the old copy.
- [ ] Update the factory seed fingerprint, generated README and checklist, and resume/verification paths that expect a brand guide. Test provisioning against the planned Strata tree and recovery of any supported older seed state.
- [ ] Remove obsolete branding guides, archive, references, and review artifacts after their active dependencies are resolved. Keep operational instructions and live generator configuration.
- [ ] Run installer, rollback, asset generation, and factory seed/recovery checks. Identify workflows that pin the shared action and stage compatible pin updates before they receive the new package format.

[Branding tree](https://github.com/sunstriker2009/sun-foundry/tree/main/branding) · [Installer](https://github.com/sunstriker2009/sun-foundry/blob/main/scripts/install-branding.py) · [Seed script](https://github.com/sunstriker2009/sun-foundry/blob/main/scripts/prepare-product-branding.sh)

## Strata

Findings: Strata has the required imagery. Its archived banner duplicates the active banner byte-for-byte. The brand guide, archive, and four reference SVGs are redundant. The manifest is missing. Foundry’s seed fingerprint has a specific dependency on Strata’s current assets and guides.

- [ ] Coordinate the template tree change with Foundry’s seed support before merging.
- [ ] Remove the brand guide, archive, and references. Fix template, setup, and asset preparation instructions that expect those paths.
- [ ] Retain the active banner, symbol, icon set, and revision directory scaffold. Add the root manifest using the agreed contract.
- [ ] Verify template CI and the coordinated seed path can remove template branding safely and produce a neutral repository without a brand guide.

[Branding tree](https://github.com/sunstriker2009/sun-strata/tree/main/branding) · [Template guide](https://github.com/sunstriker2009/sun-strata/blob/main/docs/TEMPLATE-GUIDE.md)

## Foundry Pilot

Findings: The generated brand guide is the only current file under branding. The root README and setup checklist refer to it. No artwork package is installed.

- [ ] Remove the scaffold guide and fix references in the README and setup checklist.
- [ ] Verify the repository remains a usable pilot with no fabricated artwork or package files. Use an approved package only if an installer validation run is separately authorized.

[Branding tree](https://github.com/sunstriker2009/sun-foundry-pilot/tree/main/branding) · [Setup checklist](https://github.com/sunstriker2009/sun-foundry-pilot/blob/main/docs/REPOSITORY-SETUP.md)

## Workbench

Findings: Workbench has the required imagery. Its guide, compatibility pointer, archive, references, and retired vector build artifacts are extra. The existing manifest predates the active W2 assets and names removed files and old source paths. The 96, 180, and 192 px icons and two social PNGs had no checked-in consumer in the audit. The build reads icon-512.png. The branding directory also has CSS/JSON design tokens and a font license.

- [ ] Replace the old manifest with one that describes the active package.
- [ ] Remove obsolete guides and pointers, archive and references, and update README and developer links. Review the old build wrapper before deleting its referenced archive.
- [ ] Confirm whether any external distribution uses the extra icons or social PNGs. Remove them if unneeded and keep the required 512 px build source.
- [ ] Preserve tokens.css, tokens.json, the font license, and revision snapshots. Verify the app build and any packaging-time native icon generation.

[Branding tree](https://github.com/sunstriker2009/sun-workbench/tree/main/branding) · [Build script](https://github.com/sunstriker2009/sun-workbench/blob/main/tools/build.mjs)

## Outpost

Findings: Outpost has the required imagery. Its guides, compatibility pointer, v2 handoff, archive, and refs are extra. The canonical symbol, 1024 px icon, and versioned reference PNG are byte-identical. Preserve the symbol and required icon at their respective active paths. The archived v2 banner differs from the active banner even though the guide calls it an exact copy. The manifest is missing.

- [ ] Base the root manifest on the active banner, symbol, and icons.
- [ ] Remove the redundant reference PNG, guides, handoff, and archive. Remove or replace old README links.
- [ ] Keep approved active artwork and any package documentation that explains a live workflow. Verify the active symbol path still works for the gallery.

[Branding tree](https://github.com/sunstriker2009/sun-outpost/tree/main/branding) · [Branding ZIP workflow guide](https://github.com/sunstriker2009/sun-outpost/blob/main/docs/BRANDING-ZIP-INSTALLER.md)

## CodeFolio and MarketPilot AI

- [ ] Apply the approved package contract to CodeFolio at provisioning and asset installation. No CodeFolio repository was visible at the audit checkpoint, so there is no existing tree to trim.
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
