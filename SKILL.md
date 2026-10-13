---
name: hackbot-engineering
description: Design, build, run, and improve reliable AI-agent skills for authorized web security testing. Use when creating or auditing Claude Code skills, breaking offensive-security workflows into small steps, enforcing completion checklists, reviewing artifacts, or improving repeatability and safety of bug-bounty and penetration-testing automation.
---

# Hackbot Engineering Skill

## Purpose
Help the user engineer reliable, repeatable AI-assisted workflows for **authorized** web application security testing. Prioritize methodology, evidence, completeness, reproducibility, and human review over claims of full autonomy.

This skill is an engineering guide, not permission to test arbitrary systems. Before any active testing, confirm the target is explicitly in scope and the proposed actions are permitted. If authorization or scope is unclear, stop active testing and ask for clarification. Never fabricate authorization, evade access controls or safety systems, or perform destructive actions.

## Operating principles

1. **Human-in-the-loop by design.** Agents can miss issues, overstate severity, misread evidence, or take unsafe actions. A human must review findings and any potentially impactful test.
2. **Small, discrete skills beat giant prompts.** Split large methodologies into narrow tasks with clear inputs, outputs, and exit conditions.
3. **Checklists are completion ledgers.** Every required step must be checked only after it has actually been completed and supported by an artifact or observation.
4. **Review the work, not just the narrative.** Validate logs, output files, commands, requests, and evidence. A claim that a tool ran is not proof that it ran.
5. **Define success artifacts up front.** Specify the expected directory structure, report format, evidence, and completion criteria before execution.
6. **Use explicit tool commands.** Do not ask an agent to “run the scanner” without defining the approved executable, relevant options, scope, rate limits, and expected output.
7. **Separate discovery from analysis.** Gather and preserve evidence first; analyze it in a separate stage when that reduces complexity.
8. **Review and retry failures.** A separate review pass should identify unchecked steps, missing or empty artifacts, unsupported claims, and safe retry instructions.
9. **Use multiple approaches when justified.** Models are nondeterministic. Compare independent runs or models when the value outweighs the cost; consolidate duplicates and verify every candidate manually.
10. **Keep project output out of the skill folder.** Store artifacts in a dedicated per-assessment output directory. Do not pollute reusable skill instructions with target-specific results.
11. **Re-tune as models change.** Test new models against a small, repeatable evaluation set. Remove instructions that are no longer needed only after measuring results.
12. **No vulnerability is confirmed by model confidence alone.** Require reproducible evidence and demonstrate impact safely.

## Workflow

### Phase 1 — Scope and safety gate
- Identify the authorized target(s), allowed test types, exclusions, test window, rate limits, and data-handling requirements.
- Record the scope source and the date it was checked.
- Prefer passive collection before active requests.
- Avoid destructive actions, account changes, bulk data access, persistence, or tests that could affect availability.
- For potentially sensitive findings, stop at the minimum proof needed and escalate to the human reviewer.

If the scope gate fails, do not run active tests. Return a concise list of missing authorization or scope details.

### Phase 2 — Define the task contract
For every skill or agent, write down:
- **Goal:** one discrete job.
- **Inputs:** exact paths, domains, URLs, or prior-stage artifacts.
- **Allowed tools:** approved tools and exact executable paths where practical.
- **Constraints:** scope, rate limits, authentication assumptions, and prohibited actions.
- **Procedure:** ordered, bite-sized steps.
- **Outputs:** exact paths and formats expected.
- **Exit criteria:** measurable conditions for success or a documented blocker.
- **Failure behavior:** what to log and when to stop rather than improvise.

### Phase 3 — Break down the methodology
Use small skills with clear boundaries. Example stages for an authorized web assessment:
1. Scope validation and target inventory.
2. Passive asset and historical-data collection.
3. Browser-assisted discovery and traffic capture.
4. JavaScript collection and source-map checks.
5. JavaScript parsing and endpoint/parameter inventory.
6. Content discovery using scope-appropriate lists and rate limits.
7. Focused vulnerability checks, one category per skill.
8. Evidence validation and safe impact confirmation.
9. Independent review and remediation-quality reporting.

Do not create one huge “hack the site” skill as the only workflow. Keep vulnerability classes and data-collection stages separate where that improves focus and reviewability.

### Phase 4 — Build explicit instructions
Each skill should specify:
- Ordered Markdown checklist.
- Exact tool invocations or command templates, with placeholders clearly marked.
- Expected artifacts and non-empty output requirements.
- How to handle authentication, redirects, dynamic pages, inline scripts, lazy-loaded resources, and historical data when relevant and in scope.
- How to distinguish an observation, a hypothesis, and a confirmed vulnerability.
- A clear stop condition for out-of-scope, destructive, or uncertain actions.

Do not hard-code secrets or target credentials. Do not put target-specific authorization claims in reusable skills.

### Phase 5 — Execute and collect artifacts
- Create a new output directory for the assessment, outside the skill directory.
- Record the target, timestamp, tool version, commands, exit codes, and relevant logs.
- Preserve raw evidence before transforming or deduplicating it.
- Use bounded concurrency and rate limits.
- Confirm each tool actually ran and generated the expected output.
- If a tool is unavailable, record the blocker; do not silently replace it with an unreviewed custom implementation.

### Phase 6 — Independent review
Run a review pass (ideally independent of the worker model) that checks:
- Every required checklist item is complete or explicitly blocked.
- Every expected artifact exists and is non-empty when content is expected.
- Logs and exit codes support claims that tools ran.
- Findings cite concrete request/response or other reproducible evidence.
- Severity is justified by demonstrated impact, not speculative worst-case impact.
- Duplicates are consolidated and false positives are labeled.
- Scope and safety constraints were followed.

If review fails, produce a short, specific retry instruction naming the failed checklist items and missing artifacts. Retry only the failed, safe portions. Set a retry limit; after repeated failure, report the blocker to the user instead of looping indefinitely.

### Phase 7 — Human validation and report
For each candidate finding, include:
- Title and affected in-scope asset.
- Preconditions and test account/role, if relevant.
- Reproduction steps that are minimal and safe.
- Sanitized request/response or equivalent evidence.
- Actual demonstrated impact and limitations.
- Confidence and severity rationale.
- Remediation recommendation.

A human must review severity, scope, data exposure, and any account-impacting behavior before submission. Never claim that a report was submitted or accepted unless that actually happened.

## Suggested output layout

```text
assessment-output/
  scope/
    scope-notes.md
  inventory/
    targets.txt
    collection-log.md
  artifacts/
    raw/
    normalized/
  logs/
  findings/
    candidates.md
    evidence/
  review/
    checklist-review.md
    retry-notes.md
  report/
    draft-report.md
```

Adapt this layout to the project, but define it before running the workflow and keep outputs outside the skill folder.

## Tool invocation rules
- Use only tools installed in the user's environment and permitted by the assessment.
- Prefer exact commands and explicit flags over vague tool descriptions.
- Use placeholders such as `<IN_SCOPE_HOSTS_FILE>` rather than inventing real targets.
- Set conservative rate limits and concurrency; follow the program's stated rules.
- Do not bypass bot protection, authentication, or safety controls unless the written scope explicitly authorizes the specific test method. If access is blocked, record it and ask the human reviewer.
- Do not brute-force credentials, alter real user accounts, delete records, or access/retain unnecessary sensitive data.
- Never create fake authorization documents or misrepresent permission to a model, service, or target.

## Completion standard
A workflow is complete only when all required checklist items are checked, required artifacts are present, review has passed or blockers are explicitly documented, and a human has reviewed the resulting findings. “The agent says it finished” is not a completion criterion.

## Reference checklist
Use `checklists/run-checklist.md` for the per-run checklist and `checklists/skill-quality-checklist.md` when creating or revising a skill.
