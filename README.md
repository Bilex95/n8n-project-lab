# n8n Project Lab

A personal laboratory for designing, building, testing, and documenting [n8n](https://n8n.io) automation workflows — AI agents, integrations, and general-purpose automations — with a professional QA discipline behind every one.

## Purpose

This repository is not just a collection of exported workflow files. Every project here goes through a repeatable process: requirements → architecture → build → structural QA → execution testing → documentation → versioning. The goal is a public portfolio that demonstrates both automation development *and* serious testing rigor, not just "it ran once."

## How projects are organized

Every project lives in its own self-contained folder under [`projects/`](projects/), named after what it actually does (e.g. `ai-lead-qualification-agent/`, not `project-001/`). Nothing project-specific lives outside that folder. See [`PROJECT_INDEX.md`](PROJECT_INDEX.md) for the master list of everything built here, with status and QA state.

Each project folder contains at minimum:

| File | Purpose |
|---|---|
| `<project-name>.json` | The exported n8n workflow |
| `README.md` | What it does, architecture, setup, dependencies |
| `QA.md` | Structural checks + execution test log |
| `CHANGELOG.md` | History of meaningful changes |

Projects may also include `ARCHITECTURE.md`, `test-cases.md`, or other purpose-named docs when useful.

## How QA / testing is performed

Every project is tested in layers, and the QA doc is explicit about which layers actually ran:

1. **Structural QA** — static checks on the workflow JSON (valid JSON, no broken connections, no hardcoded secrets, error-handling present on risky nodes, naming conventions).
2. **Manual execution testing** — functional, integration, negative, edge-case, error/recovery, security, and AI-specific tests, run against a live/staging n8n instance where available.
3. **Regression testing** — whenever a workflow changes, prior tests are re-run and results recorded before the change is considered done.

Structural validation alone is never claimed as proof the workflow works. `QA.md` in each project states plainly what was inspected, simulated, executed, passed, failed, or not tested (and why, if an environment was unavailable). See [`references/testing/`](references/testing/) for the reusable QA/regression templates.

## How references are managed

[`references/`](references/) holds distilled notes and patterns pulled from external n8n resources (the official n8n repo, community workflow patterns, AI agent patterns, MCP integration notes, testing approaches) — never full clones of external repositories. Each subfolder's `README.md` records where the material came from and how it's used, so external work is never presented as original. See [`references/README.md`](references/README.md).

## Version control

Every project is committed to this repository. Commits are made as work progresses (design, build, QA, fixes), and `PROJECT_INDEX.md` is updated whenever a project is completed or its status changes. This repository is public — no real credentials, tokens, or customer data are ever committed; see `.gitignore` and the secret-scan check in `.github/workflows/`.

## Navigating this repo

- [`PROJECT_INDEX.md`](PROJECT_INDEX.md) — master list of all projects
- [`projects/`](projects/) — every individual workflow project
- [`references/`](references/) — external reference notes and patterns
- [`.github/workflows/`](.github/workflows/) — automated structural QA checks (JSON validity, secret scanning)
