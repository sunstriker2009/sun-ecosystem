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
| [SUN Rename Repository](https://github.com/sunstriker2009/sun-foundry/actions/workflows/rename-repository.yml) | FOUNDRY | Owner dispatch | Automatic Plan → validate → Apply in one job; optional read-only Plan | No separate plan review or run-ID input; existing administration access gate and protected reference PRs remain |
| [SUN Rename Product](https://github.com/sunstriker2009/sun-foundry/actions/workflows/rename-product.yml) | FOUNDRY | Owner dispatch | Public-product rename; optional same-run repository rename engine | Target + STRATA/FOUNDRY/Ecosystem only; automatic Execute or read-only Plan; existing administration/PR controls remain |
| Same-branch branding ZIP hook | Opted-in product repository; shared FOUNDRY action | Owner push of a revision ZIP on feature branches | Validate and append installed assets/revisions in the same branch | Repository-scoped token; no direct main write; PR merge remains artwork approval |
| [SUN Branding ZIP Installer](https://github.com/sunstriker2009/sun-foundry/actions/workflows/branding-zip-install.yml) | FOUNDRY | Manual | Validate a revisions or legacy inbox ZIP; propose numbered asset installation or rollback | Implicit owner + repository dropdown; `repository-administration`; Preview is read-only, Apply opens a visually reviewed squash-merge PR |
| [Register SUN Repository](https://github.com/sunstriker2009/sun-foundry/actions/workflows/register-sun-repository.yml) | FOUNDRY | Manual; also Factory post-Verify hook | Propose pending-only ecosystem catalog registration | Owner confirmation; **no** automatic ID assignment or auto-merge |
| [Sync Approved SUN Symbol](https://github.com/sunstriker2009/sun-foundry/actions/workflows/sync-approved-sun-symbol.yml) | FOUNDRY | Manual | Preview/apply sync of approved PNG to ecosystem gallery | Merged canonical branding is approved; canonical path eligible for protected squash auto-merge; legacy overrides manual |
| [Reconcile Approved SUN Symbols](https://github.com/sunstriker2009/sun-foundry/actions/workflows/reconcile-approved-symbols.yml) | FOUNDRY | Daily 08:17 UTC; manual | Compare canonical symbols on product `main` with the gallery; open a PR only when changed | `repository-symbol-sync`; confirmed catalog entries only; gallery PR protected squash auto-merge |
| [Repository gallery validation](https://github.com/sunstriker2009/sun-ecosystem/actions/workflows/repository-gallery-validation.yml) | Ecosystem | Every PR; main pushes; manual | Universal `gallery` check: validate catalog identity, PNG integrity and generated README | Required check after governance alignment; no write operations |
| [Symbol sync validation](https://github.com/sunstriker2009/sun-foundry/actions/workflows/symbol-sync-validation.yml) | FOUNDRY | Relevant PR paths | Syntax, PNG and safety-invariant checks for canonical sync/reconciliation | Read-only CI; no merge decision |

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

No manual Preview or upload-to-main merge is needed. Review the resulting branding PR and squash-merge it to approve the artwork; existing daily/manual registry reconciliation then applies. WORKBENCH and OUTPOST are opted in; WORKBENCH completed the real installation pilot. A branch created before adoption needs the hook workflow before uploading to `branding/revisions/` can trigger it. Protected `main` remains PR-only; other SUN repositories need their own opt-in PR.

The hook uses the repository’s `GITHUB_TOKEN` (Contents write, Actions write and Pull requests read), not an administration PAT or environment. It refuses stale branch tips and never force-pushes. Because token-authored commits do not trigger normal push/PR CI events, an already-open PR receives explicit dispatches of its configured CI/title workflows; opening a PR afterward triggers ordinary checks. Adopters must support these dispatches with equivalent validation. See the [installer guide](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/BRANDING-ZIP-INSTALLER.md) for details and manual rollback.

### Manual fallback: install or roll back a branding ZIP

1. Upload the original ZIP to the **target repository’s** `branding/revisions/` through a normal upload PR and merge it for the manual fallback. The legacy `branding/inbox/` is also accepted. Example: `branding/revisions/strata.zip`. This stages the package; active artwork has not changed.
2. Run **SUN Branding ZIP Installer** from FOUNDRY `main`, choose the short target name, operation `preview` and the ZIP basename. Leave confirmation and rollback empty. The owner is always implicit. No Plan run ID is needed.
3. Review the changed paths, target commit and proposed revision. Run `apply` with the same filename and short-name confirmation. Review the resulting branding PR’s artwork and checks, then squash-merge it.
4. The first install backs up the existing asset tree as `branding/revisions/v1.zip` and records the installed tree as `v2.zip`. Later installs use `v3.zip` onward. Failed validation preserves the original upload name and consumes no revision; an identical package creates no PR or revision.
5. To roll back, set **Rollback revision** to an existing `v1.zip`, `v2.zip`, etc. Filename is ignored. Preview, then Apply and review/merge its PR. Restoring a snapshot creates another new version; historical ZIPs remain immutable.

The manual fallback also accepts the legacy committed inbox because dispatch forms cannot attach files. Packages are limited to 20 MB compressed and use `branding/assets/` at the ZIP root or beneath one enclosing export folder. Icons remain under `branding/assets/icons/`. The installer changes the asset tree, revision snapshots and consumed inbox upload only. Repository intro text, app-specific copies/configuration and legacy archive cleanup remain explicit follow-up work. Merging the installation PR approves the artwork for the normal daily/manual registry reconciliation; no digest approval gate is added.

An existing `chore/branding-install` branch blocks another Apply. Merge it, or close/delete it before retrying. If target branding or revision history changes while its PR is pending, recreate the proposal from current main. For exact package requirements, safety limits and failure recovery see the [branding ZIP installer guide](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/BRANDING-ZIP-INSTALLER.md). WORKBENCH completed a live installation; the live rollback/restore pilot remains pending.

### Rename a product, optionally its repository

Use **SUN Rename Product** with the current short repository name and new public product name. The pipeline derives the old name and stable SUN ID from the Ecosystem registry. Repository rename defaults off; enabling it also requires the new short repository name.

Execute automatically prepares product-name references, registry/catalog metadata and a superseding naming decision, then proposes one combined PR per changed repository. Optional repository rename invokes the existing repository-rename engine in the same run, without a second dispatch or a broader scan. Both pipelines scan only **the target + STRATA + FOUNDRY + Ecosystem**, deduplicating a governance target. Existing upfront administration credential access and PR check/review/squash controls remain.

Technical names, namespaces, data formats, env/IPC identifiers, profile locations and historical records are preserved. Source display rewriting is conservative; retained matches, native packaging and baked-in artwork may need follow-up. The automatic combined ORYVA → OUTPOST run [43934714433](https://github.com/sunstriker2009/sun-foundry/actions/runs/43934714433) succeeded; OUTPOST #175, FOUNDRY #70 and Ecosystem #37 are merged. STRATA had no diff. The first attempt failed content-write preflight before rename; a credential permission correction enabled the retry. See the [product rename operating guide](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/PRODUCT-RENAME.md). No paused product schedule is resumed.

### Rename a repository

Dispatch **SUN Rename Repository** on FOUNDRY main with the old/new short names. Default operation `execute` generates a plan, validates it and applies it automatically in one job. Select `plan` for read-only preview. No Plan run ID, second dispatch or separate plan approval is needed. Existing `repository-administration` credential approval, if configured, occurs before the job starts.

Content trees/commits are prepared across the target and deduplicated STRATA/FOUNDRY/Ecosystem before renaming to detect content-write failures early; default heads and identities are rechecked. This cannot guarantee later branch/PR permissions or atomic cross-repository completion. Execute records the plan, proposed diff and outcome in `repository-rename-run`, then opens reference PRs under the existing review/check/squash policy. It does not auto-merge them.

Product identity, namespaces, binary artwork and revision ZIPs stay unchanged. FOUNDRY self-renames remain blocked while it hosts shared Actions. The live ASTELVO → WORKBENCH pilot exposed a post-rename content-write 403 and stale gallery ordering; this update covers those cases. The shared engine then succeeded in the automatic combined ORYVA → OUTPOST pilot (run 43934714433); its three migration PRs are merged. The standalone workflow was not separately rerun during cleanup. See the [operating and recovery guide](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/REPOSITORY-RENAME.md). No live rename or paused product schedule is started by adopting this change.

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
| FOUNDRY `repository-administration` | `SUN_REPO_ADMIN_TOKEN` | Owner-gated Factory, maintenance, registration, manual symbol sync, fleet audit, governance alignment, branding ZIP PRs and rename pipelines |
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



## Cleanup and resumption checkpoint — 2026-11-16

The paired cleanup PRs retire the legacy symbol-sync approval alias/wrapper, redundant standalone repository-rename validator and historical approval-ledger validator. The combined [Rename pipeline validation](https://github.com/sunstriker2009/sun-foundry/blob/main/.github/workflows/product-rename-validation.yml) retains both rename test suites and triggers for both rename workflows. Canonical symbol safety/PNG validation and universal required FOUNDRY `build` / Ecosystem `gallery` remain. The historical ledger, archives, numbered revisions and Actions run history remain intact. See the [retirement record](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/WORKFLOW-CLEANUP.md).

**Known gap:** OUTPOST's branding hook dispatches `ci.yml` only; required `reservation` is in `master-concurrency-tests.yml`, which lacks dispatch support. Installation before opening a PR triggers ordinary checks; an already-open PR needs equivalent reservation dispatch support and a controlled final-tip pilot. This is a source-confirmed gap, not a live failure observed during cleanup.

Live rollback/restore, broader individual hook adoption, retained product display/packaging/artwork references and non-atomic rename recovery remain tracked in [issues and gaps](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/ISSUES-AND-GAPS.md). Resume from the [FOUNDRY handoff](https://github.com/sunstriker2009/sun-foundry/blob/main/docs/GOVERNANCE-HANDOFF.md) and [Ecosystem handoff](../governance/HANDOFF.md) after merging cleanup PRs. Verify current external state first. Functional development and recurring WORKBENCH/OUTPOST schedules remain paused. No memory/chat state is needed to interpret those committed checkpoints.
