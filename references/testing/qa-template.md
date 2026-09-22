# QA Template

Copy this into a new project's `QA.md` and fill it in. Only include test categories that actually apply to the project — don't blindly run every category against every workflow. Never mark something "Passed" or "Executed" unless it actually was; if an environment was unavailable, say so.

---

## Structural QA

Static checks on `<project-name>.json`, run before any execution testing.

| Check | Result | Notes |
|---|---|---|
| Valid JSON | | |
| No broken/missing node connections | | |
| No duplicate or invalid node IDs | | |
| Required trigger configuration present | | |
| No hardcoded secrets / API keys / tokens | | |
| Credentials referenced by name only (not inline) | | |
| Node naming is descriptive | | |
| Error-handling (`onError` / error workflow) present on risky nodes | | |
| Webhook/trigger config reviewed | | |
| AI-agent/tool configuration reviewed (if applicable) | | |

> Structural validation does **not** prove the workflow works. It only rules out obvious defects before execution testing.

## Manual Execution Testing

Only run against a real/staging n8n instance. If none was available, state that explicitly instead of marking tests "Passed."

**Environment:** _(e.g. local n8n v1.x, staging, unavailable — state which)_

| Test ID | Category | Objective | Preconditions | Input | Expected | Actual | Pass/Fail | Notes |
|---|---|---|---|---|---|---|---|---|
| TC-01 | Functional | | | | | | | |

### Categories to consider (include only what applies)

- **Functional** — does it do the intended job end-to-end?
- **Integration** — does it correctly talk to each external system (API, Sheets, DB, email, webhook, AI model, MCP/tool, etc.)?
- **Negative** — missing/invalid data, API failure, auth failure, external service down, malformed AI output, downstream node failure.
- **Edge-case** — empty input, null values, duplicates, oversized input, unusual characters/formats, timeouts, rate limits, partial responses.
- **Error/recovery** — retries, timeout handling, failure paths, idempotency on duplicate executions, logging, notifications.
- **Security** — credential exposure, auth/authz, webhook abuse, sensitive data leakage, insecure config, prompt injection, malicious input.
- **AI-specific** — prompt consistency, hallucination handling, structured output validity, tool selection correctness, incorrect tool args, prompt injection, unexpected model responses, context handling, fallback behavior.

## Regression Testing (on every change)

1. What changed:
2. Tests re-run related to the change:
3. Previously-passing tests re-verified:
4. Result recorded here, and in `CHANGELOG.md`:

## Summary

- **Structural QA:** Pass / Fail / Partial
- **Execution testing:** Executed / Simulated / Not Executed (environment unavailable) / Not Applicable
- **Overall QA status:** _(matches the value to record in `PROJECT_INDEX.md`)_
- **Known issues / not tested:**
