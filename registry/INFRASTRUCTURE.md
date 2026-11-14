# SUN Governance & Infrastructure Registry v1.1

**Updated:** 2026-11-14

Governance and shared engineering infrastructure use the **SUN-GNNN** identifier series. This is separate from confirmed products, which use **SUN-NNN**. IDs are assigned sequentially only when a repository/component is formally established; proposed entries do not reserve numbers.

| ID | Component | Public identity | Purpose | Repository | Classification |
|---|---|---|---|---|---|
| SUN-G001 | **SUN Ecosystem** | SUN — The Product Ecosystem | Parent governance, branding, product registry and standards | [sun-ecosystem](https://github.com/sunstriker2009/sun-ecosystem) | Governance authority |
| SUN-G002 | **STRATA** | STRATA by Sun — Structure. Foundation. Growth. | Reusable repository template and standard starting structure | [sun-strata](https://github.com/sunstriker2009/sun-strata) | Repository template |
| SUN-G003 | **FOUNDRY** | FOUNDRY by Sun — Build. Standardize. Launch. | Repository creation, governance application, CI seeding and verification | [sun-foundry](https://github.com/sunstriker2009/sun-foundry) | Repository factory |

**Next governance/infrastructure ID:** SUN-G004.

## Numbering governance

1. **SUN-NNN** identifies approved independent products/platforms; **SUN-GNNN** identifies established governance, templates, tooling and shared ecosystem infrastructure.
2. Assign the next sequential ID **upon confirmation/establishment**, never when a candidate is merely proposed.
3. Keep IDs permanent across renaming or repository relocation; do not reuse retired IDs. Corrections require an explicit documented decision.
4. SUN-G classification does **not** imply a runtime dependency on the SUN Ecosystem repository. STRATA and FOUNDRY remain independently versioned repositories.
5. Do not introduce additional prefix series without an explicit governance decision.

The [product registry](PRODUCTS.md) is authoritative for SUN-NNN assignments. The [machine-readable registry](products.json) contains both series. Implementation and releases remain in each component's own repository.
