# SUN workflow handbook

[Foundry's workflow handbook](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/WORKFLOWS.md) covers SUN registration, repository provisioning, governance, branding installation, symbol synchronization, and renames. Product repositories own their own build and deployment workflows.

## Ecosystem workflows

| Workflow | Trigger | Purpose |
| --- | --- | --- |
| [Install branding ZIP on this branch](../../.github/workflows/branding-auto-install.yml) | Owner pushes an unnumbered ZIP under `branding/revisions/` on a feature branch | Install SUN parent artwork with the shared, pinned Foundry action. See [branding and gallery](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/WORKFLOWS.md#branding-and-gallery). |
| [Repository gallery validation](../../.github/workflows/repository-gallery-validation.yml) | Every PR, main pushes, and manual dispatch | Keep the required `gallery` check and validate that the README links to Foundry’s portfolio and registry files. Foundry checks catalog identity, PNG integrity, and gallery rendering. |

Shared pull request and release rules are in the [SUN Git Workflow & Merge Policy](../governance/GIT-WORKFLOW.md).
