# Resources for Research Projects with AI Agents

A small collection of reusable materials for academic and research-oriented repositories that use AI agents as part of the writing, coding, analysis, or project-maintenance workflow.

The repository is intended for researchers, statisticians, data scientists, and maintainers of academic projects who want practical scaffolding for reproducible, reviewable, AI-assisted work. The contents are examples and starting points, not a complete project template.

## Contents

- [`AGENTS.md`](AGENTS.md) — general instructions for AI agents working in research, data science, manuscript, technical-report, analysis, or drafting repositories.
- [`prompts/`](prompts/) — reusable prompts for academic, research, and repository-maintenance workflows.
- [`scripts/git-hooks/`](scripts/git-hooks/) — optional Git hooks for enforcing local repository hygiene.
- [`README.md`](README.md) — this overview.

## How to use this repository

Copy or adapt the files that are relevant to a specific project. Do not assume that every instruction here should be used unchanged in every repository.

A typical use pattern is:

1. Review [`AGENTS.md`](AGENTS.md) and copy it into a project that will be edited by an AI coding or research agent.
2. Edit the copied `AGENTS.md` so that it reflects the project's actual data, workflow, privacy constraints, citation requirements, and maintenance rules.
3. Use prompts from [`prompts/`](prompts/) as task-specific starting points, then revise them for the project, discipline, and desired output.
4. Install or reference the Git hooks in [`scripts/git-hooks/`](scripts/git-hooks/) if they match the project's local workflow.

These materials are deliberately conservative. They emphasize research integrity, reproducibility, provenance, privacy, small reviewable edits, and explicit human review for high-risk changes.

## AI-agent instructions

[`AGENTS.md`](AGENTS.md) is written for repositories where an AI agent may edit code, analysis files, manuscripts, documentation, or other project materials.

It asks agents to treat the repository as a research record rather than only a codebase. Its main priorities are:

- protecting data, privacy, and secrets;
- preserving reproducibility and provenance;
- keeping claims, analyses, outputs, and citations traceable;
- making small, reviewable changes;
- preferring correctness and auditability over speed.

It also includes guidance on research integrity, generated files, dependency management, decision logging, manuscript standards, and when to stop for human confirmation.

Use it as a base file. Project-specific repositories should still define their own details, including accepted workflows, protected data locations, analysis commands, reporting standards, and review requirements.

## Prompts

The [`prompts/`](prompts/) directory is for reusable prompts related to academic and research workflows. These prompts are intended to help structure agent-assisted work such as repository setup, project critique, manuscript review, workflow planning, or handoff between agents.

Prompts should be treated as editable templates. Before using one, check whether it correctly reflects:

- the project's discipline and research design;
- the current repository structure;
- the available data and documents;
- the intended level of human review;
- any privacy, authorship, citation, or publication constraints.

Do not use generic prompts to make scientific, statistical, clinical, legal, ethical, or authorship decisions without appropriate human review.

## Git hooks

The [`scripts/git-hooks/`](scripts/git-hooks/) directory contains optional local Git hooks.

Currently documented hooks include:

- [`scripts/git-hooks/commit-msg`](scripts/git-hooks/commit-msg) — checks ordinary commit messages against a limited Conventional Commits 1.0.0-style subject-line format.
- [`scripts/git-hooks/pre-commit`](scripts/git-hooks/pre-commit) — blocks commits that would add or modify staged files greater than or equal to 100 MiB.

These hooks are local Git hooks. They are not automatically active just because this repository contains them.

To install a hook in another repository, copy the relevant file into that repository's `.git/hooks/` directory and make it executable. For example:

```bash
cp scripts/git-hooks/commit-msg .git/hooks/commit-msg
chmod +x .git/hooks/commit-msg

cp scripts/git-hooks/pre-commit .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

Run these commands from the repository where you want the hooks installed, adjusting the source path as needed.

Notes:

- The `commit-msg` hook validates the first non-empty, non-comment line of a commit message.
- The `commit-msg` hook allows common Git-generated merge or branch-integration messages.
- The `pre-commit` hook checks staged file content, not unstaged working-tree files.
- These hooks are local safeguards, not a substitute for CI checks, branch protection, review, or repository-hosting limits.

## Related research skills

The original README linked to an external collection of academic research skills:

<https://github.com/Imbad0202/academic-research-skills-codex>

That link is preserved here because it reflects the intended use of this repository: supporting research-focused AI-agent workflows. Review external skills before use and adapt them to the specific project rather than treating them as automatic authority.

## Status and limitations

This repository is an evolving collection of tools and templates. It is not a complete framework, package, or reproducible research environment.

Known limitations and assumptions:

- The materials assume Git-based project workflows.
- The Git hooks are shell scripts and are most directly suited to Unix-like shell environments. Windows users may need Git Bash, WSL, or equivalent shell support.
- The prompts and `AGENTS.md` provide process guidance, not scientific validation.
- The repository does not currently document a formal release process.
- No contribution guide was present when this README was drafted. Open an issue, pull request, or contact the maintainer before assuming a preferred contribution workflow.

## License

This repository is licensed under the GNU Affero General Public License v3.0. See [`LICENSE.md`](LICENSE.md) for the full license text.

In brief, AGPL-3.0 permits use, copying, modification, and redistribution under copyleft terms, and includes source-sharing obligations for modified versions made available over a network. This summary is provided for orientation only; the license file controls.

## Disclaimer

The materials in this repository are provided for general research workflow support and are not legal, medical, regulatory, statistical, or research-ethics advice. They may be incomplete, inappropriate for a specific project, or unsuitable for a particular institution, journal, funder, dataset, or regulatory setting.

Users are responsible for reviewing, adapting, validating, and maintaining any prompts, agent instructions, scripts, or workflow materials before using them in real research projects. Use appropriate human review for scientific claims, statistical methods, privacy protections, authorship decisions, citations, compliance requirements, and public releases. Use of this project and any associated dashboard, code, data products, or outputs is at the user’s own risk. To the maximum extent permitted by applicable law, the maintainer disclaims responsibility and liability for any decisions, actions, omissions, losses, damages, or consequences arising from use of, reliance on, or inability to use the project or its outputs.

## Maintenance and contact

Maintainer: Zane Billings <wz.billings@gmail.com>

This repository is intended to remain practical and lightweight. Additions should be clear, reusable, and grounded in actual academic or research workflow needs.
