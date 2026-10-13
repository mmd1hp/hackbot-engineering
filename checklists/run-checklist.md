# Hackbot Assessment Run Checklist

Use one copy per assessment. Do not check an item until it is actually complete. If an item cannot be completed, record the reason and evidence in the notes.

## A. Scope and safety
- [ ] Confirm written authorization and identify the source of scope.
- [ ] List exact in-scope hosts, applications, accounts, and environments.
- [ ] Record excluded assets, prohibited techniques, test window, rate limits, and data rules.
- [ ] Confirm the planned actions are permitted; stop and ask if anything is unclear.
- [ ] Define a stop/escalation condition for unexpected sensitive data or service impact.

## B. Task contract and setup
- [ ] Define the goal and boundaries for each agent/skill.
- [ ] Define inputs, allowed tools, constraints, outputs, and exit criteria.
- [ ] Create a dedicated assessment output directory outside the skill folder.
- [ ] Record tool versions, timestamps, and relevant configuration.
- [ ] Verify tools are installed and available; log missing tools instead of silently improvising.

## C. Collection and discovery
- [ ] Start with passive collection where practical.
- [ ] Capture required live observations and preserve raw artifacts.
- [ ] Where relevant and permitted, account for inline scripts, external scripts, lazy-loaded resources, and authenticated views.
- [ ] Where relevant and permitted, inspect historical artifacts and source maps without exceeding scope.
- [ ] Record commands, exit codes, logs, and output paths.
- [ ] Apply agreed rate limits and bounded concurrency.
- [ ] Stop if the workflow would perform a prohibited or destructive action.

## D. Analysis
- [ ] Split complex work into discrete, focused analysis tasks.
- [ ] Separate observations from hypotheses and confirmed findings.
- [ ] Record affected endpoint, parameter, role, and preconditions where applicable.
- [ ] Avoid assuming that a discovered endpoint is vulnerable merely because it exists.
- [ ] Use safe, minimal validation and avoid unnecessary access to sensitive data.
- [ ] Keep raw evidence and derived analysis separate.

## E. Artifact validation
- [ ] Every expected output path exists.
- [ ] Every expected non-empty artifact contains meaningful content.
- [ ] Logs and exit codes support claims that tools actually ran.
- [ ] Evidence is reproducible and sanitized.
- [ ] Missing artifacts and failed steps are listed explicitly.

## F. Independent review
- [ ] Review every required checklist item; mark incomplete items as failed or blocked.
- [ ] Check for unsupported claims, false positives, and duplicate findings.
- [ ] Check severity against demonstrated impact, not hypothetical impact.
- [ ] Check that scope and safety rules were followed.
- [ ] Generate a specific retry note for failed safe steps.
- [ ] Retry only the failed steps, within a defined retry limit.
- [ ] Escalate repeated failures or uncertain safety issues to the human reviewer.

## G. Human validation and reporting
- [ ] A human has validated each reportable finding.
- [ ] Each finding has minimal reproduction steps and concrete evidence.
- [ ] Impact, confidence, severity rationale, and limitations are stated accurately.
- [ ] Sensitive values and personal data are removed or minimized.
- [ ] Remediation guidance is included.
- [ ] The human reviewer approved the final report before submission.
- [ ] Submission/acceptance status is reported only if actually known.

## Final status
- [ ] Complete: all required steps passed and human review is complete.
- [ ] Complete with blockers: remaining gaps are documented and communicated.
- [ ] Incomplete: one or more required steps remain unverified.

### Notes / blockers
- Scope source and date:
- Output directory:
- Failed or blocked checklist items:
- Retry count:
- Human reviewer / review date:
