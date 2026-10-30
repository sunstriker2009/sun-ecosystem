# SUN Git Workflow & Merge Policy

**Version:** 1.0  
**Status:** Approved  
**Effective:** 2026-10-30  
**Scope:** SUN ecosystem, ORYVA by Sun, MarketPilot AI, and future SUN product repositories  
**Authority:** SUN ecosystem governance; owner: `sunstriker2009`

This document is the **authoritative** cross-repository Git workflow policy. Product repositories should link here rather than maintain divergent copies. Repository-specific CI check names and reviewer rules may vary, but must satisfy the minimum controls below. This policy is normative; documenting a requirement does **not** configure GitHub settings automatically.

## 1. Merge strategy

**Squash merge is the required default and only permitted merge method for pull requests into protected default branches.** Each PR represents one logical change; PR titles must be usable as the resulting squash commit subject.

| GitHub repository setting | Required value |
|---|---|
| Allow squash merging | Enabled |
| Allow merge commits | Disabled |
| Allow rebase merging | Disabled |
| Allow auto-merge | Enabled |
| Automatically delete head branches | Enabled |

Prefer a clean, linear `main` history. Merge only when all configured protections are satisfied. Do not use direct pushes, bypass merges, or manual cherry-picks as an alternative to the PR process without an approved, recorded exception.

## 2. Branch protection and required CI

Protect `main` through a GitHub ruleset or branch protection. Require:

1. Pull requests for all changes; prohibit direct pushes to `main` including routine maintainer pushes.
2. Required status checks to pass before merge; failures, cancellations, and pending checks must block merging.
3. Branches to be up to date with the protected base before merging (strict checks, or equivalent merge queue protections).
4. Review conversations to be resolved before merge.
5. Bypass permissions to be narrowly restricted and documented; routine work must not bypass protections.
6. Explicit human review for security-sensitive changes, including authentication, authorization, credentials, identity infrastructure and security policies.

**Required check setup:** First ensure CI workflows run on `pull_request` (and any merge-queue events if used). Run the workflow at least once so GitHub can discover the actual job/check names. Configure the branch rule with the **exact check names** emitted by CI, including any job suffixes, and select the expected GitHub Actions source where supported. Do not confuse workflow names with job check names. Ensure checks run for the PR merge candidate and are not unintentionally skipped by path filters; skipped required jobs can leave checks pending indefinitely. Verify with a deliberately failing test PR that merging and auto-merge are blocked. Recheck protections whenever CI job names change.

Administrators and automation actors must follow the same protections unless a narrowly scoped, explicitly approved exception is documented.

## 3. Pull request workflow

`Feature branch → Pull request → CI validation → Review (when required) → Squash merge → Delete feature branch`

Create short-lived, descriptive branches using these prefixes:

- `feature/<description>`
- `fix/<description>`
- `refactor/<description>`
- `docs/<description>`
- `chore/<description>`
- `hotfix/<description>`

Prefer small, focused PRs with a clear problem statement, implementation summary, tests/validation, risk notes and linked issue/ADR when appropriate. Keep the branch updated and resolve review conversations before merging. If CI fails, fix it; do not disable or bypass the check to force a merge.

## 4. Conventional Commits

Use Conventional Commits for PR titles and squash commit subjects:

`<type>(<optional-scope>): <imperative summary>`

Examples:

- `feat(auth): implement OIDC authentication`
- `fix(bootstrap): prevent duplicate master provisioning`
- `refactor(core): simplify identity abstractions`
- `test(security): add authorization integration tests`
- `docs(architecture): document Keycloak integration`
- `chore(ci): improve build pipeline`

Common types: `feat`, `fix`, `refactor`, `test`, `docs`, `chore`, `build`, `ci`, `perf`, `revert`. For breaking changes use `!` before the colon (for example, `feat(api)!: remove legacy endpoint`) or a `BREAKING CHANGE:` footer explaining impact and migration. The squash merge commit title should match the PR title; the body can include the rationale and breaking-change footer.

## 5. Auto-merge

Enable auto-merge for routine changes once all branch protections, required CI checks and applicable approvals are satisfied. **Auto-merge must never bypass failed CI.**

The following require explicit review before merge: security-critical work; authentication/authorization changes; production infrastructure changes; breaking public API changes; and significant architectural changes. Auto-merge may be used for these only **after** required reviews and approvals are completed. Apply enforceable review gates through CODEOWNERS, rulesets, required reviewers or equivalent controls rather than relying only on a checklist.

## 6. Versioning and releases

Independently released SUN products use Semantic Versioning (`MAJOR.MINOR.PATCH`):

- **MAJOR:** incompatible/breaking API changes.
- **MINOR:** backward-compatible functionality.
- **PATCH:** backward-compatible bug fixes.

Maintain a changelog and create **annotated release tags** on the protected default branch. Product-specific release procedures may add checks, approvals and artifact-signing requirements. Do **not** enable automated publishing or releases until release pipelines, secrets management and approval requirements have been designed and approved.

## 7. Scope, ownership and exceptions

This policy applies to `sun-ecosystem`, `sun-oryva`, `marketpilot-ai` and future SUN product repositories. The authoritative version lives in `sun-ecosystem/docs/governance/GIT-WORKFLOW.md`; product repositories may link to it. Their implementation details and configuration changes must be handled in their respective repositories.

Exceptions require **explicit owner approval** before use, documented with: affected repository, exact deviation, business/technical rationale, risks, compensating controls, approver, approval date and expiration/review date. Emergency exceptions must be time-bounded and reviewed retrospectively. No exception is implicit from having admin privileges.

## 8. Repository adoption and verification checklist

Track implementation **per repository**, not merely policy publication:

- [ ] Squash only; merge commits and rebase disabled.
- [ ] Auto-merge and automatic head-branch deletion enabled.
- [ ] `main` protected; PRs mandatory; bypass tightly restricted.
- [ ] Exact CI status checks configured and passing; strict up-to-date requirement enabled.
- [ ] Failing-CI PR verified to block merge and auto-merge.
- [ ] Conversation resolution required.
- [ ] Explicit review controls enforced for sensitive changes.
- [ ] Conventional Commit PR titles and squash subjects followed.
- [ ] SemVer/changelog/tag process adopted where releases exist.
- [ ] Release automation gated until approved.

**Governance milestone:** Policy documentation approval is separate from verifying each repository's live GitHub settings. Maintain adoption evidence in product-specific project tracking, not in this high-level ecosystem repository.
