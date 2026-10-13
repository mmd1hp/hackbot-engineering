# Hackbot Engineering

A Claude Code skill for designing, auditing, and reviewing reliable AI-assisted workflows for **authorized web security testing**.

It turns lessons from agentic security testing into practical engineering habits: narrow task contracts, ordered checklists, explicit output artifacts, independent review, bounded retries, and human validation.

## Why this exists

An agent saying “done” does not prove that it completed the work. Long prompts can lead to skipped steps, missing logs, empty output directories, overstated severity, and unverified findings.

Hackbot Engineering helps you define what completion means before a workflow runs—and how to verify it afterward.

## What's included

```text
.
├── SKILL.md
└── checklists/
    ├── run-checklist.md
    └── skill-quality-checklist.md
```

- **`SKILL.md`** — guidance for building, running, and improving security-agent workflows.
- **`checklists/run-checklist.md`** — assessment setup, execution, evidence, and review checklist.
- **`checklists/skill-quality-checklist.md`** — quality gate for newly created or audited skills.

## Install

Copy the folder into your Claude Code personal skills directory:

```bash
mkdir -p ~/.claude/skills/hackbot-engineering/checklists
cp SKILL.md ~/.claude/skills/hackbot-engineering/
cp checklists/*.md ~/.claude/skills/hackbot-engineering/checklists/
```

Run those commands from the extracted project directory. Restart Claude Code if the skill is not detected.

## Use it

### Build a new stage

```text
/hackbot-engineering
Create a skill for the “JavaScript collection and endpoint extraction” stage.
Output: a task contract, ordered checklist, and output layout.
Tools available: [list installed tools]
```

### Audit an existing skill

```text
/hackbot-engineering
Audit this skill against the skill quality checklist. List gaps and propose fixes without editing files yet:
[paste SKILL.md]
```

### Set up an assessment

```text
/hackbot-engineering
Scope source: [program policy URL, checked today]
Set up an output directory and run checklist for this authorized, in-scope target: [target]
```

### Review output after a run

```text
/hackbot-engineering
Review ./assessment-output against the run checklist. Identify unproven steps, missing or empty artifacts, unsupported findings, and safe retries.
```

If `/hackbot-engineering` is not recognized in your Claude Code setup, invoke the skill by name in a normal prompt.

## Design principles

1. Keep each skill focused on one discrete job.
2. Define inputs, allowed tools, constraints, outputs, exit criteria, and failure behavior.
3. Treat checklists as completion ledgers—not decorative documentation.
4. Verify artifacts and logs instead of trusting the agent's summary.
5. Separate execution from independent review when practical.
6. Retry only failed, safe steps, with a bounded retry limit.
7. Treat AI findings as candidates until reproducible evidence supports them.
8. Keep target-specific scope and assessment output out of reusable skill files.
9. Require human review of impact, severity, and potentially consequential tests.

## Safety and scope

This project is intended for authorized security testing, such as assets explicitly in scope under a bug bounty program or a written penetration-test engagement. Confirm scope, restrictions, rate limits, and data-handling requirements before active testing. Do not use the skill to justify testing systems without permission. Avoid destructive actions and stop when authorization or scope is unclear.

## Limitations

This skill is a workflow-engineering aid, not a guarantee of vulnerability discovery, complete coverage, or accurate severity. Tool availability, model behavior, and results vary. Human validation remains necessary.

## Contributing

Issues and pull requests are welcome for improvements to task contracts, checklist design, evidence requirements, and reproducibility. Please do not submit secrets, private target details, or sensitive assessment artifacts.

## License

No license has been selected yet. Until a license is added, standard copyright applies and reuse permissions are not automatically granted. Choose and add a license before inviting reuse.
