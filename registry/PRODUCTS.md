# SUN Product Registry v1.1

**Updated:** 2026-11-14. Product IDs are assigned sequentially **only upon confirmation** (SUN-001, SUN-002, ...), and remain stable after assignment except for explicitly recorded corrections. Proposals do not reserve IDs or authorize repository creation.

| ID | Name | Purpose | Status | Technical identity |
|---|---|---|---|---|
| SUN-001 | **ORYVA** | Identity, authentication, authorization, security | **CONFIRMED** | Sun.Security |
| SUN-002 | **ASTELVO** | Interactive scripting workspace and saved connections | **CONFIRMED** | Sun.Workspace |

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

## SUN-002 — ASTELVO
- **Public identity:** ASTELVO by Sun
- **Tagline:** Organize. Script. Explore.
- **Name:** Confirmed by product owner 2026-11-12 ("Sounds good, kick off").
- **Technical identity:** Sun.Workspace; Sun.Workspace.*; @sun-workspace/*.
- **Repository:** [sun-astelvo](https://github.com/sunstriker2009/sun-astelvo) (established).
- **Initial scope:** Local code and scripting workspace with folders, tags, smart collections and planned language-aware JavaScript, Python and C# execution adapters. Database connections and Kubernetes support are future extensions; see the product roadmap.
- **Extension direction:** Additional execution providers and transports; implementation planning belongs in the product repository.
- **Commercial clearance:** PENDING. Preliminary exact-name web screening only; trademarks, domains and package availability have not been cleared.
