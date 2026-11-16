# SUN Workflow Handbook

**Purpose:** central operator reference for SUN repository automation. Executable GitHub Actions remain in their owning repositories. This handbook covers the **shared SUN governance and FOUNDRY workflows**; product-specific build/deploy workflows are maintained by each product and are not claimed to be exhaustively inventoried here.

**Start here:** [FOUNDRY Actions](https://github.com/sunstriker2009/sun-foundry/actions) · [SUN Ecosystem Actions](https://github.com/sunstriker2009/sun-ecosystem/actions) · [FOUNDRY operational notes](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/WORKFLOWS.md) · [Git governance policy](../governance/GIT-WORKFLOW.md).

## Operational workflow catalog

| Workflow | Owner / launch | Trigger | Purpose | Gate and merge behavior |
|---|---|---|---|---|
| [Repository Factory](https://github.com/sunstriker2009/sun-foundry/actions/workflows/repository-factory-v1.yml) | FOUNDRY | Manual | Create or resume STRATA-based SUN repository, seed CI and enforce governance | Owner confirmation + `repository-administration`; seed PR reviewed/squash-merged |
| [Repository Maintenance](https://github.com/sunstriker2009/sun-foundry/actions/workflows/repository-factory-resume.yml) | FOUNDRY | Manual | Diagnose, plan, apply or verify governance for existing repository | Owner-controlled; never assume unsupported private-repo enforcement |
| [SUN Governance Fleet Audit](https://github.com/sunstriker2009/sun-foundry/actions/workflows/governance-fleet-audit.yml) | FOUNDRY | Manual | Read-only audit of the explicit SUN allowlist; summary and JSON results | Owner + `repository-administration`; drift returns exit 2; no settings changed |
| [SUN Governance Alignment](https://github.com/sunstriker2009/sun-foundry/actions/workflows/governance-alignment.yml) | FOUNDRY | Manual | Plan → Apply → Verify for explicitly mapped existing ruleset IDs | Owner + `repository-administration`; Apply requires a reviewed Plan run ID, matching live state and short-name confirmation |
| [SUN Rename Repository](https://github.com/sunstriker2009/sun-foundry/actions/workflows/rename-repository.yml) | FOUNDRY | Manual | Rename a configured repository and propose scoped reference updates | Owner + `repository-administration`; reviewed Plan and exact old/new confirmation; reference PRs require review and squash merge |
| Same-branch branding ZIP hook | Opted-in product repository; shared FOUNDRY action | Owner push of a revision ZIP on feature branches | Validate and append installed assets/revisions in the same branch | Repository-scoped token; no direct main write; PR merge remains artwork approval |
| [SUN Branding ZIP Installer](https://github.com/sunstriker2009/sun-foundry/actions/workflows/branding-zip-install.yml) | FOUNDRY | Manual | Validate an inbox ZIP; propose numbered asset installation or rollback | Implicit owner + repository dropdown; `repository-administration`; Preview is read-only, Apply opens a visually reviewed squash-merge PR |
| [Register SUN Repository](https://github.com/sunstriker2009/sun-foundry/actions/workflows/register-sun-repository.yml) | FOUNDRY | Manual; also Factory post-Verify hook | Propose pending-only ecosystem catalog registration | Owner confirmation; **no** automatic ID assignment or auto-merge |
| [Sync Approved SUN Symbol](https://github.com/sunstriker2009/sun-foundry/actions/workflows/sync-approved-sun-symbol.yml) | FOUNDRY | Manual | Preview/apply sync of approved PNG to ecosystem gallery | Merged canonical branding is approved; canonical path eligible for protected squash auto-merge; legacy overrides manual |
| [Reconcile Approved SUN Symbols](https://github.com/sunstriker2009/sun-foundry/actions/workflows/reconcile-approved-symbols.yml) | FOUNDRY | Daily 08:17 UTC; manual | Compare canonical symbols on product `main` with the gallery; open a PR only when changed | `repository-symbol-sync`; confirmed catalog entries only; gallery PR protected squash auto-merge |
| [Sync Merged SUN Branding (legacy approval entry)](https://github.com/sunstriker2009/sun-foundry/actions/workflows/propose-symbol-approval.yml) | FOUNDRY | Manual | Compatibility entry point for canonical symbol sync | Owner + `repository-administration`; delegates to canonical sync; no separate approval-ledger PR |
| [Repository gallery validation](https://github.com/sunstriker2009/sun-ecosystem/actions/workflows/repository-gallery-validation.yml) | Ecosystem | Every PR; main pushes; manual | Universal `gallery` check: validate catalog identity, PNG integrity and generated README | Required check after governance alignment; no write operations |
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

1. Publish or update `branding/assets/symbol.png` through the product repository's branding PR, recording provenance and visual approval.
2. Review and merge that branding PR. The merge approves the canonical artwork for registry synchronization; no separate digest-approval PR is required.
3. Allow daily **Reconcile Approved SUN Symbols** to process it, or dispatch reconciliation manually. It opens a protected squash-auto-merge gallery PR only when the catalog icon differs. SHA-256 is change-detection metadata, not an approval gate.

### Automatic branding installation on a feature branch

Opted-in repositories run the shared FOUNDRY action after an owner commits one unnumbered ZIP to `branding/revisions/` on a feature branch. The action validates the package, snapshots old assets as `v1.zip` when needed, installs the assets and writes `v2.zip` onward in a follow-up commit **on that same branch**. The original upload name is removed only on successful installation. `vN.zip` snapshots are ignored to prevent recursion. Invalid or multiple pending packages remain untouched; fix the upload and commit again.

No manual Preview or upload-to-main merge is needed. Review the resulting branding PR and squash-merge it to approve the artwork; existing daily/manual registry reconciliation then applies. The first adopter is ASTELVO. A branch created before adoption needs the hook workflow before uploading to `branding/revisions/` can trigger it. Protected `main` remains PR-only; other SUN repositories need their own opt-in PR.

The hook uses the repository’s `GITHUB_TOKEN` (Contents write, Actions write and Pull requests read), not an administration PAT or environment. It refuses stale branch tips and never force-pushes. Because token-authored commits do not trigger normal push/PR CI events, an already-open PR receives explicit dispatches of its configured CI/title workflows; opening a PR afterward triggers ordinary checks. Adopters must support these dispatches with equivalent validation. See the [installer guide](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/BRANDING-ZIP-INSTALLER.md) for details and manual rollback.

### Manual fallback: install or roll back a branding ZIP

1. Upload the original ZIP to the **target repository’s** `branding/inbox/` through a normal upload PR and merge it. Example: `branding/inbox/strata.zip`. This stages the package; active artwork has not changed.
2. Run **SUN Branding ZIP Installer** from FOUNDRY `main`, choose the short target name, operation `preview` and the ZIP basename. Leave confirmation and rollback empty. The owner is always implicit. No Plan run ID is needed.
3. Review the changed paths, target commit and proposed revision. Run `apply` with the same filename and short-name confirmation. Review the resulting branding PR’s artwork and checks, then squash-merge it.
4. The first install backs up the existing asset tree as `branding/revisions/v1.zip` and records the installed tree as `v2.zip`. Later installs use `v3.zip` onward. Failed validation preserves the original upload name and consumes no revision; an identical package creates no PR or revision.
5. To roll back, set **Rollback revision** to an existing `v1.zip`, `v2.zip`, etc. Filename is ignored. Preview, then Apply and review/merge its PR. Restoring a snapshot creates another new version; historical ZIPs remain immutable.

The manual fallback also accepts the legacy committed inbox because dispatch forms cannot attach files. Packages are limited to 20 MB compressed and use `branding/assets/` at the ZIP root or beneath one enclosing export folder. Icons remain under `branding/assets/icons/`. The installer changes the asset tree, revision snapshots and consumed inbox upload only. Repository intro text, app-specific copies/configuration and legacy archive cleanup remain explicit follow-up work. Merging the installation PR approves the artwork for the normal daily/manual registry reconciliation; no digest approval gate is added.

An existing `chore/branding-install` branch blocks another Apply. Merge it, or close/delete it before retrying. If target branding or revision history changes while its PR is pending, recreate the proposal from current main. For exact package requirements, safety limits and failure recovery see the [branding ZIP installer guide](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/BRANDING-ZIP-INSTALLER.md). The first live installation/rollback pilot is pending the installer rollout.

### Rename a repository

Run **SUN Rename Repository** on FOUNDRY main with the current and proposed short names and operation `plan`. Review `summary.md`, `references.diff` and the Plan artifact. Apply requires its successful run ID and exact confirmation `old-name -> new-name`, with unchanged repository IDs/heads and the same current FOUNDRY commit. The existing administration environment gate applies.

Apply changes the repository name, then opens reference-update PRs across the configured SUN scope. Review and squash-merge these promptly, then verify CI, registry/gallery and governance. The rename and PR merges are not atomic. Product identity, namespaces, artwork and revision ZIPs remain unchanged. FOUNDRY self-renames are blocked while it hosts shared Actions. External services, Pages, package URLs, local remotes and open branches need inspection. Live rename validation remains pending. See the [full operating and recovery guide](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/REPOSITORY-RENAME.md). No rename runs or paused development schedules are started by adopting this workflow.

### Align governance and find the Plan run ID

1. Open **SUN Governance Alignment** on `main`. Choose a short repository name such as `sun-foundry` and operation `plan`; leave the Apply-only fields empty. The owner is implicitly `sunstriker2009`.
2. Approve the administration environment if prompted. Wait for the Plan run to succeed and inspect its before/after diff and `governance-alignment-plan` artifact.
3. Open that successful run's page. The numeric value after `/actions/runs/` in its URL is the **Plan run ID**. It identifies this particular workflow execution; PR numbers, commit hashes and display run counters identify different objects.

Example from a successful FOUNDRY Plan:

```text
https://github.com/sunstriker2009/sun-foundry/actions/runs/43751547708
```

The Plan run ID in that example is `43751547708`. Use the ID from **your selected successful Plan**, rather than reusing this example for later work. Each new Plan execution has its own run ID.

4. Start a new alignment run with the same repository and the following Apply fields:

| Input | Example value |
| --- | --- |
| Repository | `sun-foundry` |
| Operation | `apply` |
| Plan run ID | `43751547708` — replace with your reviewed Plan's run ID |
| Confirmation | `sun-foundry` |

5. Apply downloads the exact Plan artifact using this ID, confirms it belongs to the same repository, and compares the plan with current policy and live state before writing. It verifies the readback automatically. Run the fleet audit afterward for the consolidated report.

Plan artifacts expire after seven days. Run a fresh Plan if its artifact expires or governance/policy changes. Apply and Verify runs also produce artifacts, but Apply accepts only a successful **Plan** artifact. Paste numeric digits; the workflow trims surrounding whitespace and rejects malformed IDs. When workflow code has been fixed, start a new dispatch on `main` to use the new version.

See the [alignment operating guide](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/GOVERNANCE-ALIGNMENT.md) and [short-name input guide](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/WORKFLOW-INPUTS.md).

### Run a one-off gallery synchronization

Use **Sync Approved SUN Symbol**, first `preview`, then `apply`. The member must be confirmed in the catalog, and the canonical artwork must have been approved through its merged branding PR. Canonical `branding/assets/symbol.png` changes can request protected squash auto-merge; legacy paths remain manual. Never use this to approve unreviewed artwork.

### Troubleshoot a failed workflow

Inspect the specific GitHub Actions run and PR checks. For Factory interruption use **Repository Maintenance** or Factory resume; do not delete or overwrite an ambiguous seed branch. For symbol failures, check the merged canonical PNG, registration status, verify required token permissions and environment configuration, and inspect whether an existing sync branch is blocking a retry. Do not bypass CI or governance to clear failures.

## Credentials and environments

| Environment | Secret | Usage |
|---|---|---|
| FOUNDRY `repository-administration` | `SUN_REPO_ADMIN_TOKEN` | Owner-gated Factory, maintenance, registration, manual symbol sync, fleet audit, governance alignment and branding ZIP PRs |
| FOUNDRY `repository-symbol-sync` | `SUN_SYMBOL_SYNC_TOKEN` | Unattended approved-symbol reconciliation; environment restricted to `main`, no required reviewers |

Store token values **only in GitHub Actions secrets**. Grant only the repository access and permissions needed. Do not commit or paste tokens into PRs. Token expiration/rotation is an operator responsibility.

## Rules that must not be automated away

- New SUN IDs, names, classifications, and product registrations require explicit governance approval.
- New or changed artwork requires human visual review and a merged product branding PR.
- Gallery sync may auto-merge only for eligible canonical sources and after GitHub's configured required checks/reviews.
- Protected `main`, feature branches, squash-only merges and automatic branch deletion remain the default.
- Do not create disposable repositories or run mutation-heavy fleet tests without explicit approval.
- Keep scheduled checks low-frequency and path-filter PR CI to conserve GitHub Actions minutes.

## Source of truth and maintenance

- [SUN product registry](../../registry/products.json) — confirmed identities.
- [SUN repository gallery catalog](../../registry/repositories.json) — repository entries and synchronized icons.
- [Historical SUN symbol approval ledger](../../registry/symbol-approvals.json) — retained historical data; current synchronization does not use it as an approval gate.
- [FOUNDRY workflow guide](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/WORKFLOWS.md) — operational implementation details.
- [SUN Git workflow governance](../governance/GIT-WORKFLOW.md) — authoritative merge and review policy.

When adding, renaming, retiring or materially changing a shared workflow, update **this handbook in the same PR or a paired ecosystem PR**. Product-specific workflows may be linked from here in a later fleet inventory; they are not automatically discovered by this document.

## Ecosystem required-check rollout

Rollout completed across the five-repository fleet; the operator reported the final audit successful. Keep the following ordering for future policy changes.

The existing repository-gallery workflow now emits the stable `gallery` job on every PR and `main` push, without path filters. It is a lightweight, standard-library-only validation of the shared registry and generated gallery; documentation-only PRs receive the same check.

Merge this workflow change and confirm it passes before merging the paired FOUNDRY policy update that expects `gallery` for `sun-ecosystem`. Then run governance alignment Plan → Apply for `sun-ecosystem`, followed by fleet audit. This updates the existing explicitly mapped ruleset; it does not create a second ruleset.
