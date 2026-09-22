# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Stack

Existing: a single static `index.html` (inline CSS + JS) deployed to GitHub Pages at https://alligator.sh (CNAME). No build step, no framework. The redesign stays a static single page so the deploy path is unchanged.

## Users

Developers who run agentic coding and code-review tools and want those agents to have persistent, source-backed context for their repositories on infrastructure they control. OpenAI Codex is the named first client; the page repeatedly says "Codex and other clients", so MCP clients in general are the audience. *(Inferred from the page copy; the session user is redesigning on behalf of the project owner and did not confirm audience details.)*

Situation: evaluating whether Alligator is real and worth waiting for, before a public CLI exists. The only action available today is joining a launch-notification list.

## Product Purpose

Alligator is a self-hosted "code context engine": it indexes a Git repository (or a workspace of related repositories), builds hybrid search indexes and a dependency graph, enriches them with commit history, and serves everything to agents through MCP. Success on this surface: a developer understands what it does, believes it is real and serious, and leaves an email for the CLI launch.

## Positioning

"The what, where, and why of your codebase" in one MCP surface: hybrid search (dense embeddings + BM25) answers *what*, the dependency graph (callers, callees, imports, cross-repository paths) answers *where*, and first-class commit history with optional LLM summaries answers *why*. Self-hosted, read-only tool surface, you own the data. Neighbors offer search or a graph; the claim is all three, persistent, on your infrastructure.

## Operating Context

- Pipeline (owner's own framing): Index → Enrich → Serve → Investigate.
- Index: point at a local checkout or Git URL; language-aware extraction with tree-sitter; Qdrant (vectors), ArangoDB (graph), Redis; incremental re-indexing with file watching and Git URL sync; resumable batches with checkpoint recovery; workspace scope across related repos.
- Enrich: optional LLM commit summaries and history embedding.
- Serve: MCP server (FastMCP) over stdio or HTTP; 11 core read-only tools including `search_code`, `find_dependencies`, `investigate_code`, plus retrieve-source and index-health tools; registered with e.g. `codex mcp add alligator -- alligator serve`.
- Investigate: find an implementation, trace dependencies, inspect the changes behind it; graph export and an interactive HTML graph view.
- Bring your own embedding and LLM providers; local models run locally, API-backed embeddings/summaries send selected content to the chosen provider.
- Owner-authored CLI lines on the current page: `alligator --help`, `alligator index ./my-monorepo --name platform`, `codex mcp add alligator -- alligator serve`.
- The three user questions the owner wrote: "Where is retry backoff implemented?" (find), "What depends on this function?" (review), "Why did this behavior change?" (understand).

## Capabilities and Constraints

- Status: private alpha. Public CLI release coming to PyPI. The CLI is Apache-2.0 licensed; the source repository remains private. Both facts must appear, once, resolved together rather than contradicting.
- Launch readiness (owner-published, updated 18 September 2026): 16 of 22 named launch checks complete. Indexing + recovery 3/4 (pending: large-repository acceptance); Search + graph 3/4 (pending: large-repository retrieval verification); MCP tool surface 4/4; CLI + operations 3/4 (pending: long-running deployment acceptance); Docs + installation 3/4 (pending: public PyPI installation verification); Public launch 0/2 (pending: package published, public installation journey verified).
- Conversion: email → Formspree endpoint `https://formspree.io/f/xojgaogg` (POST JSON `{email, source}`); promise is launch + major releases only, unsubscribe anytime.
- No public docs URL, GitHub repository, PyPI package, or demo index exists yet. Do not link to any.
- Session decision (2026-09-22): the page stays **claims-only**. No fabricated tool output, graph renders of named repositories, metrics, customers, benchmarks, or testimonials. Illustration of the mechanism is allowed only where a visitor could not mistake it for a real artifact.

## Brand Commitments

- Name: Alligator. Domain: alligator.sh. Descriptor: Code Context Engine. Creator credit: Ompragash (LinkedIn https://linkedin.com/in/Ompragash, X https://x.com/ompragash_v).
- Codex attribution: "Built and evolved alongside Codex." with the unmodified OpenAI product mark (`assets/openai-codex-product-mark.webp`), credited as the development tool, never as Alligator branding or a partnership claim; footer disclaimer "Codex and the OpenAI mark belong to OpenAI. Alligator is an independent project." must survive.
- No logo, wordmark, or motif exists.
- Standing preference (2026-09-22, recorded after a full-replacement redesign was rejected): keep the incumbent dark identity. Orbitron display, Share Tech Mono labels, Rajdhani body, cyan `#00e5ff` accent with green and amber as status colors, the particle-graph canvas, scanlines, and the custom cursor are brand commitments. The motion, above all the animated canvas, is the part valued most; refinements fix defects inside this look rather than replacing it.

## Evidence on Hand

- Only asset: `assets/openai-codex-product-mark.webp` (attribution).
- Owner-written copy in the current `index.html` (feature descriptions, pipeline steps, workflow questions, readiness checklist, CLI lines) is the content source of truth.
- Absent, and must not be invented: screenshots, real tool responses, real graph exports, docs, repo links, install verification, user quotes, numbers beyond the readiness checklist and "11 core tools".

## Product Principles

- Prove seriousness through honesty and structure, not decoration: the dated readiness checklist is the page's strongest trust asset.
- One action, one name: the launch list is called the same thing everywhere.
- Speak from the developer's chair: lead with the questions agents get asked, then the mechanism that answers them.
- Precision and provenance are the product; the surface must read as precise and traceable.
- Nothing shipped that a stress-tester could catch as fake.

## Accessibility & Inclusion

Keep and extend what the current page does right: `prefers-reduced-motion` disables every animation and the hero visualization; visible focus rings on all interactive elements; live-region form feedback; keyboard reachability. Text contrast AA minimum; functional text never below 12px; tap targets at least 44px on mobile.
