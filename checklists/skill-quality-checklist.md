# Skill Design and Quality Checklist

Use this checklist whenever you create or revise an agent skill.

## Definition
- [ ] The skill has a specific name and a short, accurate description.
- [ ] The goal is narrow enough to be completed reliably in one run.
- [ ] Inputs and prerequisites are explicit.
- [ ] Authorized-use and stop conditions are explicit.
- [ ] The skill does not assume authorization or invent target details.

## Methodology
- [ ] The procedure is ordered and broken into small steps.
- [ ] A Markdown checklist tracks actual completion.
- [ ] Every step has a verifiable completion condition.
- [ ] Tool calls use explicit commands/options where appropriate.
- [ ] Failure and unavailable-tool behavior is documented.
- [ ] The skill distinguishes discovery, analysis, validation, and reporting.

## Outputs
- [ ] Exact output directory and filenames are defined.
- [ ] Expected artifacts and formats are described.
- [ ] Raw evidence is preserved separately from derived results.
- [ ] Logs, exit codes, and timestamps are captured where useful.
- [ ] The skill writes assessment artifacts outside its own reusable folder.

## Review and reliability
- [ ] A reviewer checks checklist completion and output existence.
- [ ] Non-empty files are checked for meaningful content, not just existence.
- [ ] Findings require concrete evidence and safe reproduction.
- [ ] Severity is based on demonstrated impact.
- [ ] Retries are bounded and target failed steps only.
- [ ] Human review is required for security conclusions and risky actions.

## Evaluation and maintenance
- [ ] The skill is tested on a small, authorized, repeatable evaluation set.
- [ ] False positives, missed steps, empty artifacts, and unsafe behavior are recorded.
- [ ] Model/tool changes are tested before changing the methodology.
- [ ] Redundant instructions are removed only after testing confirms they are unnecessary.
- [ ] The skill description is concise and avoids unnecessary sensitive context.
