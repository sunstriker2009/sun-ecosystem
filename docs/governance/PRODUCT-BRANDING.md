# SUN Product Repository Branding Standard

**Version:** 2.1  
**Effective:** Upon merge  
**Status:** Approved direction — product-specific assets require owner approval  
**Scope:** SUN repository branding packages, new and existing. The SUN parent-brand exception is in section 5.  
**Implementation:** [Foundry branding installer](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/BRANDING-ZIP-INSTALLER.md)

This standard complements the [SUN Brand Guidelines](../../branding/BRAND-GUIDELINES.md), [SUN Visual Identity](../../branding/VISUAL-IDENTITY.md) and [Git Workflow & Merge Policy](GIT-WORKFLOW.md).

## 1. Concept and approval

Before finalizing assets, produce concept artwork for explicit owner review. Each concept should:

- Integrate a recognizable visual connection to the Sun into the design. Choose a cue that fits the product’s form or imagery, such as a sunrise arc, sunlight, or another recognizable expression of the Sun.
- Communicate the product's **core purpose** through its central symbol.
- Where natural, subtly suggest the **first character** of the public product name.
- Use its [product-family visual theme](../../branding/BRAND-GUIDELINES.md#product-families-and-visual-themes) and a **distinct product palette and silhouette** to differentiate it within the portfolio.
- Maintain consistent family typography, optical weight, proportions, spacing and professional finish. Use the **“by Sun”** endorsement in the endorsed lockup and README banner.

**Priority:** product purpose and immediate recognizability outweigh forcing a letter shape. Avoid generic symbols, excessively complex motifs and confusing similarity to other SUN products. Do not imply approval from an exploratory image.

Capture the approved family, palette, typography, accessibility considerations and usage restrictions in the artwork review when they matter for future use. Preserve any supporting font, license and style files used by the product.

## 2. README panoramic banner

Place an **approved, high-resolution panoramic image** at the top of each product README. It must contain:

- Product symbol and product name. Set the name in **ALL CAPS** in the banner artwork (for example, **CODEFOLIO**). Use the [approved display casing](../../branding/NAMING-GUIDELINES.md#display-names-and-artwork) in README headings, prose, and image alt text.
- **“by Sun”** endorsement.
- Approved product tagline.

Use an appropriate wide composition (16:9 or wider where suitable) that stays legible at normal GitHub README widths, including mobile. Preserve aspect ratio; do not stretch or crop essential text. Commit the actual image into the repository; do not depend on temporary image-generation URLs or external hosts.

Keep the README image at the stable path `branding/assets/readme-banner.png` when revising the artwork.

## 3. Canonical artwork and derivative assets

The **owner-approved original artwork is the canonical visual source of truth**. Preserve the original unmodified, preferably with source/layer files or a transparent export of the symbol. Where feasible, extract the actual symbol and its SUN cue from that source for high-resolution, transparent raster assets rather than independently redrawing them.

- Derive high-resolution standalone marks, app illustrations and raster icons from the approved symbol source, preserving the intended material, gradient, lighting and proportions.
- Prefer a transparent original or layered source for clean extraction. Cropping a flattened banner can include glow, background and compositing artifacts; do not claim an exact transparent extraction without checking it.
- Treat vector SVGs as **purpose-built adaptations** where resolution independence, monochrome, accessibility or tiny UI sizes require simplified geometry. Label adaptations as such, and review them against the canonical artwork.
- Never substitute a visually similar regenerated image or third-party image for the approved original.
- Review icons at their actual output sizes. Adapt the chosen SUN cue for small sizes as needed. For example, increase a sunrise arc’s weight or improve the contrast of a sunlit detail. Retain export scripts and supporting style files where they serve an active workflow.

## 4. Compact and production assets

Use approved **PNG** compact assets that stay consistent with the banner and canonical symbol. Provide complementary SVG adaptations only where a concrete application, monochrome, accessibility or scaling need justifies them; SVG is not a universal delivery requirement. Where SVG variants are adopted, consider:

- Full horizontal lockup and standalone symbol.
- Light, dark and monochrome variants.
- Simplified small-size variants, including a legible icon at practical UI sizes.
- Appropriate app-icon exports (for example PNG sizes or platform-specific exports).

Compact assets should carry forward the banner’s recognizable symbol, chosen SUN cue, palette logic, and typography in a form suited to their display size. Avoid embedding raster artwork inside an SVG as a substitute for a vector icon.

## 5. Branding package layout

Use stable filenames that describe the asset’s purpose.

```text
branding/
  assets/
    readme-banner.png
    symbol.png
    concept-artwork.png     # Optional
    icons/
      icon-16.png
      icon-24.png
      icon-32.png
      icon-48.png
      icon-64.png
      icon-128.png
      icon-256.png
      icon-512.png
      icon-1024.png
  revisions/
  manifest.json
```

- The banner, canonical PNG symbol, and nine square PNG icons are required. Each icon’s actual dimensions must match its filename. Keep app-specific exports, fonts, font licenses, styles, and design tokens that have active consumers.
- Use optional `branding/assets/concept-artwork.png` for the verified artwork reference used to build the package. Use the existing banner as the reference when it is the approved artwork itself.
- Maintain current product metadata in `branding/manifest.json`, including `family-id`, `product-name` and `short-description`. Maintain these values with repository identity and setup. The imagery package does not include a separate asset manifest.
- The SUN parent brand may ship a partial icon set. For temporary consistency, missing filenames may use renamed copies of the closest available approved SUN icon. The copies retain their original pixel dimensions. Exact-dimension validation applies to product packages.
- Keep numbered ZIP snapshots under `branding/revisions/`. Dedicated per-repository branding guides, branding README files, archives, reference folders, and historical review material are outside the standard layout.

## 6. Repository workflow

1. Develop and review concepts. Obtain explicit owner approval before declaring the identity final.
2. Produce the panoramic banner, symbol, and icons from the approved direction.
3. Commit the approved assets on a feature branch and update the README to reference the canonical banner path when adopting it.
4. Validate asset paths, icon dimensions, image readability, active references, and required CI. Squash merge under SUN governance.
5. Use the same canonical paths for future artwork revisions.

## 7. Existing-repository adoption

Migrate existing layouts through reviewed repository PRs. Coordinate live README references, workflows, config, installers, and downstream consumers before moving files. Review the approved concept, SUN cue, family theme, palette, typography, and legibility as part of adoption.

- [ ] Verify the approved banner uses the all-caps product name, “by Sun” endorsement, and tagline.
- [ ] Verify the canonical symbol and required icon sizes. Preserve supporting assets and any application-specific exports with active consumers.
- [ ] Check the product metadata against the repository identity.
- [ ] Move approved removals into temporary `branding/recycling/`, preserving original repository-relative paths for recovery. Exclude recycled files from installation, asset discovery, and active branding validation.
- [ ] Verify the migration across affected repositories before deleting recycling folders in a separate review.
- [ ] Coordinate the Ecosystem gallery move from `branding/registry/` to top-level `gallery/` with registry image paths, README generation, gallery validation, and Foundry publishing and reconciliation workflows.

## 8. Imagery installation and revision history

Only `branding/assets/` represents the installable imagery package. Imagery installation must write only within that directory and preserve supporting files. When the incoming package contains `preview.png`, install it as `branding/assets/concept-artwork.png`. Maintain `branding/manifest.json` and other files under the branding root separately. Create numbered ZIP snapshots and maintain revision bookkeeping separately from imagery installation. Rollback should restore assets within `branding/assets/` from the chosen snapshot.

Repositories adopting the revised installation contract must first update to a compatible Foundry installer. Existing pins follow the [current installer guide](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/BRANDING-ZIP-INSTALLER.md), including its combined installation and revision workflow, until migrated. Review artwork and required checks before the squash merge.
