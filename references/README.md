# References

Curated knowledge extracted from external n8n-related repositories — never full clones, never verbatim dumps. Each source below is tracked with its license and what this lab actually adopted from it, so external work is never presented as original.

## Categories

- **`n8n-core/`** — official n8n node/expression/platform knowledge and official skill patterns.
- **`workflow-patterns/`** — real-world workflow design patterns (triggers, branching, error handling, integrations).
- **`ai-agents/`** — AI agent architecture patterns (tool use, routing, multi-agent, browser agents).
- **`mcp/`** — MCP (Model Context Protocol) tooling for building/validating n8n workflows with an AI agent.
- **`testing/`** — reusable QA/regression templates and testing philosophy used across all projects.
- **`hosting/`** — local/production n8n deployment architecture (Docker, Postgres, Redis, queue mode, HTTPS).
- **`custom-nodes/`** — reference for building custom n8n nodes, used only when native nodes can't do the job.

## Source inventory

| Source | License | Priority | Lives in | Adopted | Explicitly NOT adopted |
|---|---|---|---|---|---|
| [n8n-io/n8n](https://github.com/n8n-io/n8n) | Fair-code (Sustainable Use License), custom — not OSI | Very High | `n8n-core/` | Node/expression/platform behavior notes, official agent guidance from `.agents/skills/`, `AGENTS.md`, `CLAUDE.md` | `packages/` full source tree, Docker/devcontainer infra, unrelated build tooling |
| [n8n-io/n8n-docs](https://github.com/n8n-io/n8n-docs) | Custom (site license, not OSI) | High | `n8n-core/` | Concepts on AI agents, tools, memory, MCP, expressions; doc-writing conventions for our own READMEs | Full docs site / GitBook build infra |
| [n8n-io/skills](https://github.com/n8n-io/skills) | Apache-2.0 | High | `n8n-core/` | Official skill patterns (referenced by czlonkowski/n8n-skills as the base its hooks adapt from) | Wholesale copy — n8n-skills already adapts this; we use it as provenance, not a second copy |
| [Zie619/n8n-workflows](https://github.com/Zie619/n8n-workflows) | MIT | High | `workflow-patterns/`, `testing/` | Representative architecture patterns; `test_workflows.py` / `test_security.sh` / `SECURITY.md` as testing/security ideas | The full workflow collection (2000+ files) — never dumped in; no workflow assumed production-ready just because this repo says so |
| [wassupjay/n8n-free-templates](https://github.com/wassupjay/n8n-free-templates) | **None (no LICENSE file — all rights reserved by default)** | Medium | `workflow-patterns/` | Pattern *ideas only* (categories, node combinations) described in our own words | **No file/JSON copying at all** — no license to permit it. Any adaptation must be rebuilt from scratch, not derived from their file content |
| [czlonkowski/n8n-mcp](https://github.com/czlonkowski/n8n-mcp) | MIT | Extremely High | `mcp/` | Installed as a project-scoped MCP server (`.mcp.json`, docs/validation-only mode — no API key, no live n8n instance connected) for node search/validation while building workflows | Deploy/execute tools (require `N8N_API_URL`/`N8N_API_KEY`) — not enabled until a real n8n instance exists |
| [czlonkowski/n8n-skills](https://github.com/czlonkowski/n8n-skills) | MIT (hooks layer adapts Apache-2.0 patterns from n8n-io/skills, see their NOTICES) | Extremely High | `mcp/` | Installed as a Claude Code plugin — 14-skill catalog covering expressions, error handling, sub-workflows, AI agents, etc. | — |
| [langbot-app/LangBot](https://github.com/langbot-app/LangBot) | Apache-2.0 | High (supporting) | `ai-agents/` | Agent/skill architecture ideas, MCP usage patterns, E2E testing structure, rate limiting/access control concepts | Full application, IM integrations, plugin marketplace, full test suite |
| [nanobrowser/nanobrowser](https://github.com/nanobrowser/nanobrowser) | Apache-2.0 | High (supporting) | `ai-agents/`, `testing/` | Planner→Navigator→Observation→Correction architecture; the core QA lesson: **"AI says success" ≠ "system state proves success"** | Browser extension implementation |
| [lemony-ai/cascadeflow](https://github.com/lemony-ai/cascadeflow) | MIT | High (supporting) | `ai-agents/` | Model-cascading/routing QA ideas: test the *routing decision*, not just final output; budget/tool-call limits | Full framework |
| [coleam00/local-ai-packaged](https://github.com/coleam00/local-ai-packaged) | Apache-2.0 | Very High (supporting) | `hosting/` | Local AI stack architecture reference (n8n+Ollama+Supabase+Qdrant+Caddy); security notes on Execute Command / filesystem access | Installing the full stack — services are added only when a project needs them |
| [n8n-io/self-hosted-ai-starter-kit](https://github.com/n8n-io/self-hosted-ai-starter-kit) | Apache-2.0 | Very High (local AI) | `hosting/` | Minimal n8n+Ollama+Qdrant+Postgres Docker Compose reference for local AI projects | Treated as PoC reference, not a production template |
| [n8n-io/n8n-hosting](https://github.com/n8n-io/n8n-hosting) | MIT | High | `hosting/` | Production deployment patterns: queue mode, Redis, Caddy/HTTPS, version pinning, upgrade-as-regression-event | Kubernetes/AWS/Helm — not introduced until a project needs them |
| [n8n-io/n8n-nodes-starter](https://github.com/n8n-io/n8n-nodes-starter) | MIT | High (specialized) | `custom-nodes/` | Custom node structure, declarative node example, `@n8n/node-cli`, custom-node QA checklist | Not used unless a project has a genuine capability gap native nodes can't fill |

## Rules for this folder

1. Never copy entire files or large verbatim blocks from a source repo — distill patterns into original notes.
2. Every subfolder's content that derives from an external source must cite it (link + license), per the table above.
3. Respect the source's license — where there is none (wassupjay/n8n-free-templates), no file content is reused, only independently-described ideas.
4. Keep notes practical — how a pattern applies to workflows built in *this* lab, not a copy of upstream docs.
5. Pattern notes inside each category folder are populated incrementally, as real projects actually draw on them — not pre-written in bulk for repos nothing has used yet.
