# SUN Workflow Handbook

**Purpose:** central operator reference for SUN repository automation. Executable GitHub Actions remain in their owning repositories. This handbook covers the **shared SUN governance and FOUNDRY workflows**; product-specific build/deploy workflows are maintained by each product and are not claimed to be exhaustively inventoried here.

**Start here:** [FOUNDRY Actions](https://github.com/sunstriker2009/sun-foundry/actions) · [SUN Ecosystem Actions](https://github.com/sunstriker2009/sun-ecosystem/actions) · [FOUNDRY operational notes](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/WORKFLOWS.md) · [Git governance policy](../governance/GIT-WORKFLOW.md).

## Operational workflow catalog

| Workflow | Owner / launch | Trigger | Purpose | Gate and merge behavior |
|---|---|---|---|---|
| [Repository Factory](https://github.com/sunstriker2009/sun-foundry/actions/workflows/repository-factory-v1.yml) | FOUNDRY | Manual | Create or resume STRATA-based SUN repository, seed CI and enforce governance | Owner confirmation + `repository-administration`; seed PR reviewed/squash-merged |
| [Repository Maintenance](https://github.com/sunstriker2009/sun-foundry/actions/workflows/repository-factory-resume.yml) | FOUNDRY | Manual | Diagnose, plan, apply or verify governance for existing repository | Owner-controlled; never assume unsupported private-repo enforcement |
| [Register SUN Repository](https://github.com/sunstriker2009/sun-foundry/actions/workflows/register-sun-repository.yml) | FOUNDRY | Manual; also Factory post-Verify hook | Propose pending-only ecosystem catalog registration | Owner confirmation; **no** automatic ID assignment or auto-merge |
| [Sync Approved SUN Symbol](https://github.com/sunstriker2009/sun-foundry/actions/workflows/sync-approved-sun-symbol.yml) | FOUNDRY | Manual | Preview/apply sync of approved PNG to ecosystem gallery | SHA-256 must match approval ledger; canonical path eligible for protected squash auto-merge; legacy overrides manual |
| [Reconcile Approved SUN Symbols](https://github.com/sunstriker2009/sun-foundry/actions/workflows/reconcile-approved-symbols.yml) | FOUNDRY | Daily 08:17 UTC; manual | Compare approved canonical digests to product `main`; open gallery PR only when needed | `repository-symbol-sync`; unapproved bytes skipped; gallery PR protected squash auto-merge |
| [Propose SUN Symbol Approval](https://github.com/sunstriker2009/sun-foundry/actions/workflows/propose-symbol-approval.yml) | FOUNDRY | Manual | Preview candidate fingerprint or propose approval-ledger PR | Owner + `repository-administration`; **manual artwork approval and merge required** |
| [Repository gallery validation](https://github.com/sunstriker2009/sun-ecosystem/actions/workflows/repository-gallery-validation.yml) | Ecosystem | Relevant PR paths; manual | Validate catalog identity, PNG integrity and generated README | Required check as configured; no write operations |
| [Symbol approval ledger validation](https://github.com/sunstriker2009/sun-ecosystem/actions/workflows/symbol-approval-validation.yml) | Ecosystem | Relevant PR paths | Validate approved symbol ledger schema, membership and digest format | Read-only; does **not** visually approve artwork |
| [Symbol sync validation](https://github.com/sunstriker2009/sun-foundry/actions/workflows/symbol-sync-validation.yml) | FOUNDRY | Relevant PR paths | Syntax and safety-invariant checks for sync and approval automation | Read-only CI; no merge decision |

For the exact workflow inputs, consult the linked workflow's **Run workflow** dialog and the current YAML on `main`. Some workflows expose additional mode-specific inputs. The catalog describes the intended current implementation; it does not assert that every check is configured as required in every repository.

## Common operator recipes

### Create a new SUN repository

1. Confirm the proposed name and identity under [SUN product registry](../../registry/PRODUCTS.md) and naming policy.
2. Run **Repository Factory** from FOUNDRY on `main`. Use STRATA as the template; allow governance verification to complete.
3. Inspect and squash-merge the product-neutral seed PR. The Factory's post-Verify hook proposes a **pending** ecosystem registration PR.
4. Review the registration and explicitly assign/confirm its SUN identity through normal governance PRs. Never auto-approve new identities.

### Approve new or revised artwork

1. Commit the proposed raster to the product repository as `branding/assets/symbol.png` through its normal PR/CI process; document its provenance and visual approval in the product brand guide.
2. Run **Propose SUN Symbol Approval** in `preview` mode with the repository repeated for confirmation.
3. Visually inspect the exact PNG on the product repository's `main`. Then use `apply` to create an ecosystem PR changing only `registry/symbol-approvals.json`.
4. **Manually review and merge** that approval PR. The digest ledger is the explicit trust boundary; no filename or product commit is approval by itself.
5. Allow **Reconcile Approved SUN Symbols** to pick up the newly approved digest, or manually dispatch reconciliation for immediate processing. It opens a gallery PR and requests GitHub native protected squash auto-merge. No PR is needed if already synchronized.

### Run a one-off gallery synchronization

Use **Sync Approved SUN Symbol**, first `preview`, then `apply`. The member must be confirmed in the catalog, and its source SHA-256 must already be in the approval ledger. Canonical `branding/assets/symbol.png` changes can request protected squash auto-merge; legacy paths remain manual. Never use this to approve unreviewed artwork.

### Troubleshoot a failed workflow

Inspect the specific GitHub Actions run and PR checks. For Factory interruption use **Repository Maintenance** or Factory resume; do not delete or overwrite an ambiguous seed branch. For symbol failures, compare product source SHA-256 against `registry/symbol-approvals.json`, check registration status, verify required token permissions and environment configuration, and inspect whether an existing sync branch is blocking a retry. Do not bypass CI or governance to clear failures.

## Credentials and environments

| Environment | Secret | Usage |
|---|---|---|
| FOUNDRY `repository-administration` | `SUN_REPO_ADMIN_TOKEN` | Owner-gated Factory, maintenance, registration, manual symbol sync and approval proposals |
| FOUNDRY `repository-symbol-sync` | `SUN_SYMBOL_SYNC_TOKEN` | Unattended approved-symbol reconciliation; environment restricted to `main`, no required reviewers |

Store token values **only in GitHub Actions secrets**. Grant only the repository access and permissions needed. Do not commit or paste tokens into PRs. Token expiration/rotation is an operator responsibility.

## Rules that must not be automated away

- New SUN IDs, names, classifications, and product registrations require explicit governance approval.
- New or changed artwork requires human visual approval and a reviewed approval-ledger PR.
- Gallery sync may auto-merge **only after** digest verification and GitHub's configured required checks/reviews.
- Protected `main`, feature branches, squash-only merges and automatic branch deletion remain the default.
- Do not create disposable repositories or run mutation-heavy fleet tests without explicit approval.
- Keep scheduled checks low-frequency and path-filter PR CI to conserve GitHub Actions minutes.

## Source of truth and maintenance

- [SUN product registry](../../registry/products.json) — confirmed identities.
- [SUN repository gallery catalog](../../registry/repositories.json) — repository entries and synchronized icons.
- [SUN symbol approval ledger](../../registry/symbol-approvals.json) — owner-approved canonical PNG fingerprints.
- [FOUNDRY workflow guide](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/WORKFLOWS.md) — operational implementation details.
- [SUN Git workflow governance](../governance/GIT-WORKFLOW.md) — authoritative merge and review policy.

When adding, renaming, retiring or materially changing a shared workflow, update **this handbook in the same PR or a paired ecosystem PR**. Product-specific workflows may be linked from here in a later fleet inventory; they are not automatically discovered by this document.
