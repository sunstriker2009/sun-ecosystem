# SUN Product Registry v1.0

**Updated:** 2026-11-12. Product IDs are stable across renames. A proposal is not an approved product or authorization to create a repository.

| ID | Name | Purpose | Status | Technical identity |
|---|---|---|---|---|
| SUN-001 | **ORYVA** | Identity, authentication, authorization, security | **CONFIRMED** | Sun.Security |
| SUN-002 | ORBIT | Workflow orchestration and coordination | PROPOSED | Sun.Orchestration (suggested) |
| SUN-003 | NOVA | AI agents and intelligent automation | PROPOSED | Sun.Agents (suggested) |
| SUN-004 | PRISM | AI intelligence, research, insights | PROPOSED | TBD |
| SUN-005 | PULSAR | Event processing and messaging | PROPOSED | TBD |
| SUN-006 | LUMEN | Analytics and visualization | PROPOSED | Sun.Analytics (suggested) |
| SUN-007 | BEACON | Monitoring and observability | PROPOSED | TBD |
| SUN-008 | FORGE | Developer tools and utilities | PROPOSED | TBD |
| SUN-009 | **ASTELVO** | Interactive scripting workspace and saved connections | **CONFIRMED** | Sun.Workspace |

STRATA and FOUNDRY are tracked as established SUN infrastructure in [INFRASTRUCTURE.md](INFRASTRUCTURE.md), not as numbered products. MarketPilot AI remains an independent application and is not part of the SUN product registry.

## SUN-001 — ORYVA
- **Public identity:** ORYVA by Sun
- **Tagline:** Identity. Trust. Protection.
- **Name:** Confirmed by product owner 2026-10-30; supersedes HALO.
- **Repository:** [sun-oryva](https://github.com/sunstriker2009/sun-oryva) (established).
- **Backend packages:** Sun.Security.*
- **Frontend packages:** @sun-security/*
- **Initial integration target:** MarketPilot AI, an independent application.
- **Visual accent:** Solar Gold (provisional).
- **Commercial clearance:** PENDING; confirmation is internal, not trademark clearance.

## Naming risk notes
The proposed names ORBIT, NOVA, PRISM, PULSAR, LUMEN, BEACON and FORGE have potential existing-software associations and require fresh conflict research before approval. PULSAR in particular overlaps with Apache Pulsar in messaging; FORGE overlaps with Atlassian Forge in developer tools.

## SUN-009 — ASTELVO
- **Public identity:** ASTELVO by Sun
- **Tagline:** Organize. Script. Explore.
- **Name:** Confirmed by product owner 2026-11-12 ("Sounds good, kick off").
- **Technical identity:** Sun.Workspace; Sun.Workspace.*; @sun-workspace/*.
- **Repository:** [sun-astelvo](https://github.com/sunstriker2009/sun-astelvo) (established).
- **Initial scope:** Local code and scripting workspace with folders, tags, smart collections and planned language-aware JavaScript, Python and C# execution adapters. Database connections and Kubernetes support are future extensions; see the product roadmap.
- **Extension direction:** Additional execution providers and transports; implementation planning belongs in the product repository.
- **Commercial clearance:** PENDING. Preliminary exact-name web screening only; trademarks, domains and package availability have not been cleared.
