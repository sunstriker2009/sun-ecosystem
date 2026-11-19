# SUN Ecosystem Map

**Status:** Current organizational relationships, not a deployment diagram.  
**Updated:** 2026-11-18

```mermaid
flowchart TD
    SUN["SUN Ecosystem — governance (SUN-G001)"]
    Strata["Strata — repository template (SUN-G002)"]
    Foundry["Foundry — repository factory (SUN-G003)"]
    Outpost["Outpost — identity and security platform (SUN-C001)"]
    Workbench["Workbench — scripting workspace (SUN-P001)"]
    MARKET["MarketPilot AI — independent application"]

    SUN -->|governs branding and policy| Strata
    SUN -->|governs branding and policy| Foundry
    SUN -->|governs branding and registry| Outpost
    SUN -->|governs branding and registry| Workbench
    Strata -->|template source| Foundry
    Foundry -.->|provisions new repositories; not a runtime dependency| Outpost
    Foundry -.->|provisions new repositories; not a runtime dependency| Workbench
    Outpost -.->|planned integration; not yet verified live| MARKET
```

## Boundaries

- **SUN Ecosystem** is the central authority for portfolio naming, brand guidelines, product registry and governance; it is not an application runtime.
- **Strata** is a reusable repository template. **Foundry** uses Strata to provision repositories and apply/verify governance. Neither is a product runtime dependency.
- **Outpost** and **Workbench** are confirmed, independently usable SUN products. Their implementation and delivery status belong in their own repositories.
- **MarketPilot AI** is an independent application and initial planned Outpost integration target; do not describe it as already powered by Outpost until verified.
- Dotted links indicate intended or illustrative relationships, **not evidence of historical provisioning or completed integration**.

## Authoritative sources

- [Product registry](../../registry/PRODUCTS.md) and [machine-readable registry](../../registry/products.json)
- [Brand architecture](../../branding/BRAND-GUIDELINES.md)
- [Repository governance](../governance/GIT-WORKFLOW.md)
- [Foundry](https://github.com/sunstriker2009/sun-foundry) and [Strata](https://github.com/sunstriker2009/sun-strata)
