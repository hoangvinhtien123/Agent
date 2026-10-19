# Code Review.md — Code Reading & Analysis Skills

> Routed from **[[1.Skills/Skills]]** by keywords: `read code`, `read the code`, `analyse code`, `analyze code`, `code review`, `review code`, `explain code`, `walkthrough`, `5.Code`, `codebase`.
> If a needed skill is missing, research it and **append below** with a clear `> [!note] Added <date> — <reason>` comment. Never overwrite existing skills.

---

# Skill: Full-Stack Repository Reading & Analysis (5.Code)

## Description
Expert skill for reading an entire source folder end to end and reporting what it does, how it is built, and where it is weak — without modifying it. Built for mixed repositories that combine an SAP backend with a non-SAP frontend and cloud runtime configuration.
- Detect the code type of every sub-folder and file (ABAP, RAP, CDS, Fiori/SAPUI5, CAP, React/TypeScript, Node, SQL, MTA/BTP config, Markdown docs, image mockups)
- Map the repository tree, entry points, and the boundary contract between layers (OData service, REST route, destination)
- Read every file in scope in batches and reconstruct the data flow from persistence to screen
- Compare a "current/fixed" source branch against an exported baseline and list what changed and why
- Extract the effective domain model (tables, entities, keys, fields, units, currencies) and the authorization model
- Identify risks: dead code, duplication, unverified fields, missing tests, inconsistent calculations, uncommitted assumptions
- Produce a structured review (Scope, Purpose, Architecture, Key logic, Dependencies, Observations, Recommendations)

## When To Use
Activate when the request contains:
- read code, read the code, analyse code, analyze code, code review, review code, explain code, walkthrough
- 5.Code, codebase, repository, folder analysis, "what does this project do"
Examples:
- "Analyse the folder in 5.Code — it has React, ABAP and RAP"
- "Read this repo and tell me the architecture and the risks"
- "Explain how the frontend talks to the backend in this project"

## Responsibilities
1. Scope — enumerate the full tree first (including sub-folders), state the file count, and exclude only build output, `.git`, `node_modules`, and secret-bearing files.
2. Detect — classify each sub-folder by extension and content signature (`.asddls`/`.asbdef`/`.acds` → RAP-CDS, `.abap` → ABAP, `.view.xml` + `manifest.json` → SAPUI5, `.cds` + `srv/` → CAP, `.tsx`/`.jsx` → React, `xs-app.json`/`mta.yaml` → BTP approuter/MTA).
3. Read — cover every file end to end, in batches for large repos; never sample, skim, or infer a file's content from its name.
4. Reconstruct — build the layer map: database tables → interface views → root/projection views → behavior definition/implementation → service definition/binding → HTTP route → client data layer → screens.
5. Cross-check — verify the frontend's assumed contract against the backend's actual fields, keys, parameters, and authorizations; list every mismatch.
6. Assess — record duplication, dead/obsolete objects, hardcoded values, missing tests, silent fallbacks, and calculations that contradict the documented behaviour.
7. Persist — append the reusable capability to the matching `1.Skills` file and the project/domain facts to `2.Knowledge`; log every file touch in `0.Logs`.
8. Report — deliver the analysis in the chat reply; recommend improvements only, never edit the source.

## Supported Artifacts
SAP backend:
- DDIC tables, CDS interface/root/projection views, view entities with parameters, behavior definitions (managed/unmanaged), behavior pools and local handler classes, access controls (DCL), service definitions and bindings, SADL virtual-element exit classes
Frontend:
- React + TypeScript sources (components, hooks, context providers, routers), SAPUI5 XML views and controllers, client-side OData V2/V4 request layers, CSV/export helpers
Runtime & config:
- `mta.yaml`, `xs-security.json`, `xs-app.json`, approuter launch scripts, destinations, `.env` samples, `package.json` scripts, Vite/TS configs
Docs & assets:
- README/setup/review Markdown, ADT export manifests, UI mockup images
Evidence sources:
- Repository docs first, then code, then naming conventions; never a filename alone

## Best Practices
Always: read the repository's own docs before judging the code; state the file count and the code types found; separate "what the code does" from "what the docs claim"; quote concrete identifiers (entity, field, function) for every finding; flag any backend object that has never been activated or verified in the target system; treat `5.Code` as read-only.
Prefer: tracing one end-to-end scenario (one screen → one entity → one table) to prove the contract; grouping findings by severity (blocking / important / nice-to-have); reporting the authorization model explicitly (objects, fields, activities, scopes); comparing baseline vs corrected source when both exist.
Avoid: reading secret files (`default-env.json`, `.env.local`, credentials), rewriting or reformatting reviewed code, guessing at a framework that has not been verified, presenting a recommendation as if it were already implemented, and reporting only a sample of a large folder.

## Output Rules
- Analyse: report Scope, Purpose, Architecture & structure, Key logic, Dependencies & integrations, Observations, Suggested improvements, and the skill/knowledge routing report.
- Explain: follow the runtime path in order (request → route → service → view → table) and name the file that implements each hop.
- Compare: give a per-object delta table (object, old behaviour, new behaviour, reason) instead of prose.
- Review: list findings with an ID, the file, the impact, and the recommended fix — recommendations only; change nothing unless explicitly asked.
- Always name the code types detected and list any file deliberately skipped and why.

---

<!-- New code review skills are appended below this line, each with a clear "Added <date> — <reason>" comment. Do not overwrite existing skills. -->
