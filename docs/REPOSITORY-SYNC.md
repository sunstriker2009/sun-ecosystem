# SUN repository gallery and synchronization contract (v1 foundation)

The authoritative product identities, SUN IDs and infrastructure classifications remain in `registry/products.json`. The separate `registry/repositories.json` is the machine-maintained display index. A repository can be `pending` with `registryId: null`; this **does not** approve its name or reserve a SUN ID.

## Catalog and icon rules

- `repository` is a unique `sunstriker2009/name` slug; `name` and `summary` are display-only. Use the [approved display casing](../branding/NAMING-GUIDELINES.md#display-names-and-artwork) for `name`.
- Confirmed `registryId`, `classification`, repository, and name must agree with `registry/products.json`. Infrastructure uses `SUN-GNNN`. Products use `SUN-PNNN` or `SUN-CNNN` according to their registered family.
- An icon is optional while branding is not approved. Never copy a template icon as a new product's identity.
- Once approved, a PNG is stored at `branding/registry/<repository-name>.png`, with its SHA-256 in `iconSha256`. The renderer checks PNG signature, file existence, hash and safe paths.
- Run `python scripts/render-repository-gallery.py` to regenerate the README section between its markers; `--check` validates it without mutation.
- Product and infrastructure tiles are separated. Pending repositories are shown separately.

## Original Foundry integration plan

1. After successful Factory governance verification, submit a `pending` catalog registration PR. Never assign SUN IDs or auto-approve identities.
2. Provide a standalone Foundry workflow with preview and apply modes for existing repositories.
3. A participating repository's approved branding change on `main` triggers a sync request; only validated PNG content is copied into this repository via a PR.
4. Keep one sync branch per repository, compare content hashes, and avoid no-op PRs.
5. Restrict auto-merge to changes in the catalog, approved icon copy, and generated gallery; require CI, and prohibit auto-merge of ID, ownership or classification changes.

Cross-repository writes need a narrowly scoped credential, preferably a GitHub App installation token. Do not grant arbitrary source repositories write access to SUN governance. No webhook server is required; GitHub Actions `workflow_dispatch` or `repository_dispatch` can coordinate the workflows.

See the [SUN Workflow Handbook](workflows/README.md) for current registration, symbol synchronization, and reconciliation workflows.
