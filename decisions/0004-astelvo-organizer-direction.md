# ASTELVO: organizer-first direction

Date: 2026-11-12
Status: Accepted — product direction and tagline
Product: SUN-009

## Decision
Retain ASTELVO by Sun and Sun.Workspace. Adopt the owner-approved tagline "Organize. Script. Explore.". Begin as a local code organizer and interactive scripting workspace: flexible folders/tags/collections, saved scripts, language-aware editing/formatting, and embedded Try It runners for JavaScript, Python and C#.

## Supersession
This revises the initial scope in decision 0003; it does not change the product ID or naming approval. Database profiles no longer own scripts. SQL Server/PostgreSQL connections, Windows database authentication and Kubernetes forwarding are future execution-target extensions, outside the first release. Keep the earlier decision as history.

## Architecture and delivery
The architecture roadmap, detailed milestones and implementation belong in sun-astelvo. Reuse sun-repo-template for file generation and sun-repo-bootstrap for governance on the generated repository. The current provisioner does not create repositories and its baseline does not enforce sensitive-change reviews; record actual enforcement separately. Shell and implementation choices remain proposed until validated.

## Clearance
Commercial naming/package/domain clearance remains pending; scope revision is not a clearance claim.
