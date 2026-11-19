# SUN Product Naming Guidelines v1.0

**Status:** Finalized internally on 2026-10-30.

## Naming principles
1. Prefer short names, ideally **4–7 letters**.
2. Favor memorable pronunciation and recognizable spelling across markets.
3. Start with the product’s purpose and audience. Consider familiar words or metaphors that explain what the product does or how people use it.
4. Invented names are welcome when distinctive and pronounceable.
5. Prefer distinctive identities over generic technical labels.
6. Maintain a recognizable SUN family identity without making names interchangeable.
7. Ensure names work in logos, websites, documentation, repositories, and packages.
8. Avoid confusingly similar existing brands, especially in overlapping software categories.
9. Check trademarks, domains, GitHub, NuGet, npm, and market usage before public commercial adoption.
10. **Only explicit owner approval confirms a product name.**

## Candidate scoring (100 points)
| Criterion | Points |
|---|---:|
| Distinctiveness | 25 |
| Domain relevance | 20 |
| Memorability | 15 |
| Pronunciation / international appeal | 10 |
| SUN family coherence | 10 |
| Visual identity potential | 10 |
| Technical naming suitability | 10 |

Scores of 85+ are preferred, but **no score overrides a material conflict**. Preliminary web research is not trademark clearance.

## Workflow
**IDEA → PROPOSED → SHORTLISTED → CONFIRMED → RELEASED**. Optional states: RESERVED, SUPERSEDED, RETIRED.

For each new concept: establish purpose and audience; decide SUN fit; propose 5–10 candidates; assess meaning, pronunciation, distinctiveness and competing brands; recommend 2–3; review domain/trademark/package availability; propose repo/namespace/package conventions; obtain explicit approval; update registry and decision log.

## Display names and artwork

Use the approved PascalCase spelling in prose, navigation, UI, registries, and gallery labels. Current examples include **Strata**, **Foundry**, **Workbench**, **Outpost**, and **CodeFolio**. Preserve intentional spaces and acronym casing in names such as **Foundry Pilot** and **MarketPilot AI**. The parent brand is **SUN**, and the endorsement is **by Sun**.

Panoramic README banner artwork uses an all-caps product name, such as **CODEFOLIO**, with the **by Sun** endorsement and the approved tagline. See the [Product Repository Branding Standard](../docs/governance/PRODUCT-BRANDING.md#2-readme-panoramic-banner).

## Technical conventions
| Surface | Pattern | Example |
|---|---|---|
| Endorsed display name | ProductName by Sun | Outpost by Sun |
| Repository | sun-product | sun-outpost |
| .NET | Sun.Capability | Sun.Security |
| NuGet | Sun.Capability.* | Sun.Security.AspNetCore |
| npm | @sun-capability/* | @sun-security/react |
| Integration | Powered by ProductName | Powered by Outpost |

Technical identifiers may stay stable even if a public product name changes. All package examples are conventions, not proof of availability.

## Commercial-clearance gate
Before a public release, investigate relevant trademark registries (including Canada and the US where applicable), competitors, domains, GitHub names, NuGet IDs and npm scopes. Record findings and seek qualified legal review where warranted. **Internal confirmation ≠ commercial clearance.**
