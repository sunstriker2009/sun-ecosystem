# SUN Product Repository Branding Standard

**Version:** 1.0  
**Status:** Approved direction — product-specific assets require owner approval  
**Scope:** All SUN product repositories, new and existing  
**Reference implementations:** [ASTELVO](https://github.com/sunstriker2009/sun-astelvo) and [ORYVA](https://github.com/sunstriker2009/sun-oryva)

This standard complements the [SUN Visual Identity](../../branding/VISUAL-IDENTITY.md) and [Git Workflow & Merge Policy](GIT-WORKFLOW.md). A product's own brand guide records approved choices; the ecosystem guide governs consistency.

## 1. Concept and approval

Before finalizing assets, produce concept artwork for explicit owner review. Each concept should:

- Incorporate the recognizable **SUN arc** as the family connection.
- Communicate the product's **core purpose** through its central symbol.
- Where natural, subtly suggest the **first character** of the public product name.
- Use a **distinct product palette** to avoid close resemblance to sibling products.
- Maintain consistent family typography, optical weight, proportions, spacing and professional finish.

**Priority:** product purpose and immediate recognizability outweigh forcing a letter shape. Avoid generic symbols, excessively complex motifs and confusing similarity to other SUN products. Do not imply approval from an exploratory image.

Record approval, rejected alternatives where useful, final palette (color values), typography, clear space, minimum sizes, contrast/accessibility considerations and usage restrictions in the product's brand guide.

## 2. README panoramic banner

Place an **approved, high-resolution panoramic image** at the top of each product README. It must contain:

- Product symbol and public product name.
- **“by Sun”** endorsement.
- Approved product tagline.

Use an appropriate wide composition (16:9 or wider where suitable) that stays legible at normal GitHub README widths, including mobile. Preserve aspect ratio; do not stretch or crop essential text. Commit the actual image into the repository; do not depend on temporary image-generation URLs or external hosts.

When replacing a production image, use a **new versioned filename** (for example, `readme-banner-v2.png`) and update the README reference to prevent stale GitHub/browser image caching. Keep old versions only when useful for provenance or documentation.

## 3. Canonical artwork and derivative assets

The **owner-approved original artwork is the canonical visual source of truth**. Preserve the original unmodified, preferably with source/layer files or a transparent export of the symbol. Where feasible, extract the actual symbol and SUN arc from that source for high-resolution, transparent raster assets rather than independently redrawing them.

- Derive high-resolution standalone marks, app illustrations and raster icons from the approved symbol source, preserving the intended material, gradient, lighting and proportions.
- Prefer a transparent original or layered source for clean extraction. Cropping a flattened banner can include glow, background and compositing artifacts; do not claim an exact transparent extraction without checking it.
- Treat vector SVGs as **purpose-built adaptations** where resolution independence, monochrome, accessibility or tiny UI sizes require simplified geometry. Label adaptations as such, and review them against the canonical artwork.
- Never substitute a visually similar regenerated image or third-party image for the approved original.
- Maintain source provenance, export scripts, dimensions and usage rules in the product brand guide. Validate small sizes and do not assume a raster crop is suitable at 16–32 px.

## 4. Compact and production assets

Provide complementary **SVG** assets for application headers, internal UI and documentation:

- Full horizontal lockup and standalone symbol.
- Light, dark and monochrome variants.
- Simplified small-size variants, including a legible icon at practical UI sizes.
- Appropriate app-icon exports (for example PNG sizes or platform-specific exports).

Compact assets must retain the same recognizable symbol, SUN arc, palette logic and typography as the panoramic banner, simplified appropriately for small placements. Avoid embedding raster artwork inside an SVG as a substitute for a vector icon.

## 5. Asset organization

Recommended product-repository structure:

```text
branding/
  BRAND-GUIDE.md
  concepts/
    concept-01.png
  assets/
    readme-banner-v1.png
    lockup-dark.svg
    lockup-light.svg
    lockup-mono.svg
    symbol-dark.svg
    symbol-light.svg
    symbol-mono.svg
    symbol-small.svg
    icons/
      app-icon-256.png
```

Naming can vary to accommodate existing repositories. **Separate exploratory concepts from approved production assets.** Keep README image references relative to repository paths. Maintain a short asset manifest in `BRAND-GUIDE.md` describing purpose, version and approved usage. GitHub Social Preview may use the same visual direction, but its upload through GitHub Settings is a separate operation.

## 6. Repository workflow

1. Develop and review concepts; obtain explicit owner approval before declaring the identity final.
2. Produce panoramic banner and coordinated compact assets from the approved direction.
3. Commit assets and the product brand guide on a feature branch; update README banner reference.
4. Open a PR, validate paths, image readability, visual consistency and required CI; squash merge under SUN governance.
5. For future revisions, keep a new versioned banner filename and update the brand guide and references in the same PR.

## 7. Existing-repository adoption

Treat existing products as an **adoption checklist**, not an assumption of compliance. Review each product independently; record missing assets and follow-up PRs in that product repository. ASTELVO and ORYVA are **reference examples**, not evidence that every item below has been completed.

- [ ] Owner-approved concept and documented SUN arc / purpose / optional initial-letter rationale.
- [ ] Distinct approved palette and consistent family typography/spacing.
- [ ] High-resolution panoramic README banner with symbol, name, “by Sun” and tagline.
- [ ] Banner committed locally with a versioned filename and readable at GitHub widths.
- [ ] SVG full lockup and standalone symbol.
- [ ] Light, dark, monochrome and small-size variants; app-icon exports.
- [ ] Canonical approved source preserved; high-resolution derivatives trace to that source.\n- [ ] Concept originals separated from production assets.
- [ ] Product brand guide documents approval, palette, typography, locations and usage rules.
- [ ] Changes merged via feature branch, CI and squash PR.

**Initial review targets:** [ASTELVO](https://github.com/sunstriker2009/sun-astelvo), [ORYVA](https://github.com/sunstriker2009/sun-oryva), [FOUNDRY](https://github.com/sunstriker2009/sun-foundry), then remaining SUN products as appropriate. No existing repository is automatically changed by adoption of this document.
