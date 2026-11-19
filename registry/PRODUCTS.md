# SUN Product Registry v1.1

**Updated:** 2026-11-18. Product IDs are assigned sequentially **only upon confirmation** (SUN-001, SUN-002, ...), and remain stable after assignment except for explicitly recorded corrections. Proposals do not reserve IDs or authorize repository creation.

| ID | Name | Purpose | Status | Technical identity |
|---|---|---|---|---|
| SUN-001 | **Outpost** | Identity, authentication, authorization, security | **CONFIRMED** | Sun.Security |
| SUN-002 | **Workbench** | Interactive scripting workspace and saved connections | **CONFIRMED** | Sun.Workspace |

## Unnumbered product proposals

| Candidate | Purpose | Status | Suggested technical identity |
|---|---|---|---|
| ORBIT | Workflow orchestration and coordination | PROPOSED | Sun.Orchestration (suggested) |
| NOVA | AI agents and intelligent automation | PROPOSED | Sun.Agents (suggested) |
| PRISM | AI intelligence, research, insights | PROPOSED | TBD |
| PULSAR | Event processing and messaging | PROPOSED | TBD |
| LUMEN | Analytics and visualization | PROPOSED | Sun.Analytics (suggested) |
| BEACON | Monitoring and observability | PROPOSED | TBD |
| FORGE | Developer tools and utilities | PROPOSED | TBD |

These names are **unapproved and unnumbered**. The next approved product receives **SUN-003**, regardless of its candidate name. Proposed names may be revised, withdrawn or approved later.

SUN Ecosystem (SUN-G001), Strata (SUN-G002), Foundry (SUN-G003), and Foundry Pilot (SUN-G004) are tracked in the separate [governance and infrastructure registry](INFRASTRUCTURE.md). They do not consume SUN-NNN product IDs. MarketPilot AI remains an independent application and is not part of the SUN product registry.

## SUN-001 — Outpost
- **Public identity:** Outpost by Sun
- **Tagline:** Identity. Trust. Protection.
- **Name:** Outpost supersedes ORYVA. ORYVA previously superseded HALO on 2026-10-30. See the [Outpost rename decision](../decisions/product-renames/sun-001-outpost.md).
- **Repository:** [sun-outpost](https://github.com/sunstriker2009/sun-outpost) (established).
- **Backend packages:** Sun.Security.*
- **Frontend packages:** @sun-security/*
- **Initial integration target:** MarketPilot AI, an independent application.
- **Visual accent:** Solar Gold (provisional).
- **Commercial clearance:** PENDING; confirmation is internal, not trademark clearance.

## Naming risk notes
The proposed names ORBIT, NOVA, PRISM, PULSAR, LUMEN, BEACON and FORGE have potential existing-software associations and require fresh conflict research before approval. PULSAR in particular overlaps with Apache Pulsar in messaging; FORGE overlaps with Atlassian Forge in developer tools.

## SUN-002 — Workbench
- **Public identity:** Workbench by Sun
- **Tagline:** Organize. Script. Explore.
- **Name:** Confirmed by product owner 2026-11-12 ("Sounds good, kick off").
- **Technical identity:** Sun.Workspace; Sun.Workspace.*; @sun-workspace/*.
- **Repository:** [sun-workbench](https://github.com/sunstriker2009/sun-workbench) (established).
- **Initial scope:** Local code and scripting workspace with folders, tags, smart collections and planned language-aware JavaScript, Python and C# execution adapters. Database connections and Kubernetes support are future extensions; see the product roadmap.
- **Extension direction:** Additional execution providers and transports; implementation planning belongs in the product repository.
- **Commercial clearance:** PENDING. Preliminary exact-name web screening only; trademarks, domains and package availability have not been cleared.
