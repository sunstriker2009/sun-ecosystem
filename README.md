![SUN — The Product Ecosystem](branding/assets/readme-banner.png)

# ☀️ SUN Product Ecosystem

**One source. Many independent products.**

This repository is the canonical reference for SUN product naming, brand architecture, visual identity direction, and recorded branding decisions. Foundry maintains SUN product and repository records. It does **not** contain application implementation or development milestones.

## SUN parent identity

The approved parent-brand banner and [symbol](branding/assets/symbol.png) represent the SUN product family. See the [SUN Brand Guidelines](branding/BRAND-GUIDELINES.md#parent-brand-artwork).

## SUN product portfolio

Explore the [repository gallery](https://github.com/sunstriker2009/sun-foundry/blob/main/registry/GALLERY.md), [product registry](https://github.com/sunstriker2009/sun-foundry/blob/main/registry/PRODUCTS.md), and [governance and infrastructure registry](https://github.com/sunstriker2009/sun-foundry/blob/main/registry/INFRASTRUCTURE.md) in Foundry. The [ecosystem relationship diagram](docs/architecture/ECOSYSTEM-MAP.md) shows how the products and shared infrastructure fit together.

## Documentation

| Document | Purpose |
|---|---|
| [Brand Guidelines v2.0](branding/BRAND-GUIDELINES.md) | SUN positioning, brand architecture and product-family visual themes |
| [Reusable Prompts](docs/prompts/README.md) | Copyable collaboration prompts, including thread continuation handoffs |
| [SUN Workflow Handbook](docs/workflows/README.md) | SUN workflow entry points and ownership |
| [Repository Factory](https://github.com/sunstriker2009/sun-foundry) | Automated repository creation, CI initialization, governance application, verification and recovery |
| [Strata — Repository Foundation](https://github.com/sunstriker2009/sun-strata) | Standard starting structure and CI workflows for new SUN repositories |
| [Git Workflow & Merge Policy v1.0](docs/governance/GIT-WORKFLOW.md) | Authoritative cross-repository PR, squash merge, CI, review and release governance |
| [Naming Guidelines v1.0](branding/NAMING-GUIDELINES.md) | Naming rules, scoring, workflow and clearance |
| [Product Repository Branding Standard v2.0](docs/governance/PRODUCT-BRANDING.md) | Approved concept workflow, README banners, PNG assets, optional SVG adaptations and existing-repository adoption checklist |
| [Outpost product documentation](https://github.com/sunstriker2009/sun-outpost) | Architecture, design system, engineering roadmap and implementation (maintained outside SUN ecosystem) |
| [Product Registry](https://github.com/sunstriker2009/sun-foundry/blob/main/registry/PRODUCTS.md) | Confirmed and proposed product names |
| [Governance & Infrastructure Registry](https://github.com/sunstriker2009/sun-foundry/blob/main/registry/INFRASTRUCTURE.md) | Governance and infrastructure identities |
| [Ecosystem Map](docs/architecture/ECOSYSTEM-MAP.md) | Mermaid diagram of current organizational relationships |
| [Machine-readable Registry](https://github.com/sunstriker2009/sun-foundry/blob/main/registry/products.json) | Structured product metadata |
| [Brand Architecture Decision](decisions/0001-sun-brand-architecture.md) | Endorsed brand model |
| [Outpost naming decision](decisions/product-renames/sun-001-outpost.md) | ORYVA → Outpost and SUN-C001 continuity |
| [Product Ideas](docs/product-ideas.md) | Early concepts and product direction |
| [Product Proposal Template](templates/PRODUCT-PROPOSAL.md) | Starting new proposals |
| [Naming Review Template](templates/NAMING-REVIEW.md) | Candidate evaluation and clearance |
| [Workbench naming decision](decisions/0004-workbench-rename.md) | SUN-P001 approval and naming rationale |
| [Changelog](CHANGELOG.md) | Version history |

## Product repository branding

SUN product repositories follow the [Product Repository Branding Standard](docs/governance/PRODUCT-BRANDING.md): product-family visual themes, purpose-led symbols with a visual connection to SUN, distinct palettes, approved panoramic README banners and coordinated PNG compact assets, with optional SVG adaptations. [Workbench](https://github.com/sunstriker2009/sun-workbench) and [Outpost](https://github.com/sunstriker2009/sun-outpost) are reference examples; existing repositories should track adoption independently.

## Repository provisioning

Use [Foundry — Repository Factory](https://github.com/sunstriker2009/sun-foundry) to create and initialize new SUN repositories from the [Strata template](https://github.com/sunstriker2009/sun-strata). The Factory provisions CI and governance, verifies supported enforcement, and supports resuming interrupted setup. [Repository Maintenance](https://github.com/sunstriker2009/sun-foundry/actions/workflows/repository-factory-resume.yml) handles existing-repository diagnosis and governance changes. For operation and limitations, see the [Factory workflow guide](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/WORKFLOWS.md). Private repositories on unsupported GitHub plans cannot be treated as strictly verified; the Factory fails closed in that case.

## Governance

Names become confirmed only after explicit owner approval. Internal naming approval does not imply trademark, domain, NuGet, npm, or GitHub availability. Visual colors and marks are provisional unless expressly approved. All changes follow the [SUN Git Workflow & Merge Policy v1.0](docs/governance/GIT-WORKFLOW.md): protected `main`, pull requests, passing required CI, applicable review, **squash-only merges**, and automatic branch cleanup. Record substantive brand decisions under `decisions/`.

**Branding policy version:** 2.0 — 2026-11-18.

## Resuming governance work

Read the [governance handoff](docs/governance/HANDOFF.md) for verified evidence, pending validation, cross-repository responsibilities and resume boundaries before continuing after thread archival.
