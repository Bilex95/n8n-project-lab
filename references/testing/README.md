# Testing Reference

Templates: [`qa-template.md`](qa-template.md), [`project-readme-template.md`](project-readme-template.md), [`changelog-template.md`](changelog-template.md) — copy these into a new project.

## Core testing philosophy for this lab

**Validation passing does not prove correctness.** Structural QA, node/workflow validation, and "it imported successfully" are necessary but not sufficient. A workflow must actually be exercised — manually or live — before its behavior is trusted.

**An AI claiming success is not evidence of success.** Distilled from [nanobrowser/nanobrowser](https://github.com/nanobrowser/nanobrowser)'s multi-agent QA lessons: verify actual downstream system state (a record was really created, an email really sent, a file really written) rather than trusting an agent's or model's self-report.

**Test the decision, not just the output**, for anything with routing/escalation logic (multi-model AI workflows): was the right model/branch chosen, not just "did it eventually produce an answer." Distilled from cascading-router QA concepts (see `references/ai-agents/`).

**Testing status must be honest**, always one of: `NOT TESTED` · `STRUCTURALLY VALIDATED` · `MANUALLY TESTED` · `LIVE EXECUTION TESTED` · `PASSED` · `FAILED` · `BLOCKED` · `NOT AVAILABLE`. Never claim a status that didn't actually happen — see [`qa-template.md`](qa-template.md).

Security- and test-script ideas (`test_security.sh`, `SECURITY.md`, `test_workflows.py`) referenced from [Zie619/n8n-workflows](https://github.com/Zie619/n8n-workflows) (MIT) inform the security-QA checklist categories in `qa-template.md` — adapted as our own checklist items, not copied scripts.
