# spec-kit-pm Development Instructions

## Project Information

- **Repository**: <https://github.com/CassandraGargoyle/spec-kit-pm>
- **Project Name**: spec-kit-pm
- **Primary Purpose**: AI-native project management specification kit — templates, AI agent instructions, and workflows for spec-driven, AI-orchestrated project execution (see [README.md](README.md))
- **Repository Type**: Documentation and specifications (Markdown only). No application code, no build system, no test suite.
- **Project Stage**: Early planning. The repository structure exists as skeletons; concrete templates, agent prompts, and workflows are still to be authored. Backwards compatibility is not a concern — restructure freely.
- **License**: MIT (see [LICENSE](LICENSE))

## Repository Structure

```text
spec-kit-pm/
  templates/        project specs, roadmap, risks, decisions, KPIs (skeletons)
    roadmap/
      gantt.md      Gantt chart spec & template (Mermaid)
  agents/           AI agent instructions (pm, reviewer, risk-analyst, reporter)
  workflows/        spec-to-plan, execution-loop
  profiles/         company / industry customization (example-company/)
  examples/         worked examples
  .markdownlint*.jsonc   Markdown linting configuration
```

## Conventions

### Language

All **persisted** content — Markdown, file names, commit messages, agent prompts — is always written in **English**. This is non-negotiable. Chat replies and ad-hoc team communication may be in any preferred language, but anything that ends up in the repository is English.

### Markdown

- Conform to the rules in `.markdownlint.jsonc` and `.markdownlint-cli2.jsonc`
- Lint with `markdownlint-cli2` before committing if you have it installed locally
- One H1 per file; use ATX headings (`#`, `##`, …); ordered lists use sequential numbering (`1.`, `1.`, `1.` rendered as `1, 2, 3` per MD029 config)

### Diagrams

- **Gantt charts MUST be authored in Mermaid.** See [`templates/roadmap/gantt.md`](templates/roadmap/gantt.md) for the full specification, required elements, and template. Image exports from MS Project / GanttProject / spreadsheet screenshots are explicitly forbidden.
- For other diagram types prefer Mermaid (<https://mermaid.js.org/>) where it is expressive enough; fall back to PlantUML or D2 only when Mermaid cannot represent the diagram.

### File Layout

- One template / agent / workflow per Markdown file
- File names use `kebab-case.md`
- A subdirectory's `.gitkeep` may be removed once a real file replaces the placeholder

### TODO Markers

Use the format `TODO:NNN [INITIALS]: description` with per-file sequential numbering (001, 002, 003, …). Use `TODO:XXX [INITIALS]: …` as a temporary placeholder when the next number is not yet known.

## Per-developer Display Language

Everything **persisted** is always English (see *Language* above). What each developer *sees on screen* — AI assistant chat replies, CLI status messages, interactive prompts — may be set to their preferred language individually:

- Add `**Display Language**: <ISO 639-1 code or English name>` to your **personal** `CLAUDE.local.md` (gitignored — never committed)
- Examples: `**Display Language**: cs` · `**Display Language**: de` · `**Display Language**: English` (default)
- If unset, English is the default
- AI assistants and locale-aware tooling SHOULD honor this; if a tool cannot, English is the safe fallback
- This setting MUST NOT change anything written to a file or sent to a remote system — only what is rendered to the developer's own terminal/chat

## AI Assistant Guidelines

This kit is itself a framework for AI-driven project management. When authoring agent instructions or workflows, dogfood the kit's own conventions.

- Do **not** add "Generated with [Claude Code]" or similar signatures to files
- Do **not** add `Co-Authored-By: Claude` (or any AI co-author trailer) to git commits
- When adding agent prompts, document **Responsibilities**, **Inputs**, and **Outputs** explicitly so the agent can be invoked deterministically
- When adding workflows, write them as numbered, reproducible step sequences with clear entry and exit criteria

## Repository Management

- Main branch is `main`
- License: MIT — see [LICENSE](LICENSE)
- GitHub remote: <https://github.com/CassandraGargoyle/spec-kit-pm>
- Recommended fork model for company customization: keep `CassandraGargoyle/spec-kit-pm` as upstream, fork into your org, rebase regularly (see README → *Upstream & Fork Model*)

## Security Guidelines

- Never run destructive commands (`rm -rf`, `git push --force`, `git reset --hard`, branch deletion) without explicit user confirmation
- Warn about potential data loss before any risky operation
- Treat the user's working tree as authoritative — investigate unfamiliar files before deleting or overwriting
