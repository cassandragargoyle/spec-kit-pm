# spec-kit-pm

**AI-native project management specification kit for defining context, decisions, workflows, and validation in modern projects.**

> **Status:** early stage. The repository structure (templates, agents, workflows, profiles, examples) is in place as skeletons — concrete templates and agent prompts are still to be filled in. See [Roadmap](#-roadmap).

---

## 🚀 Overview

**spec-kit-pm** is a lightweight, extensible framework for managing projects through **structured specifications instead of ad-hoc task management**.

It is designed for the AI era, where:

* AI generates plans, tasks, and code
* Humans focus on **context, decisions, and validation**
* Projects are driven by **specs, not tickets**

---

## 🧠 Core Principles

* **Context over tasks**
  Define *why* and *what*, not just *what to do*

* **Spec-driven execution**
  Every project artifact starts from a structured specification

* **AI-first workflows**
  AI agents generate plans, summaries, risks, and validation

* **Decision traceability**
  All key decisions are recorded and auditable

* **Asynchronous collaboration**
  Minimize meetings, maximize clarity

---

## 📦 What’s Included

* 📄 **Templates**

  * Project spec
  * Roadmap
  * Risk register
  * Decision log (ADR-like)
  * KPI / success metrics

* 🤖 **AI Agent Instructions**

  * PM agent
  * Reviewer agent
  * Risk analyst agent
  * Reporting agent

* ⚙️ **Workflows**

  * Spec → Plan → Execution → Validation
  * AI-assisted task generation
  * Continuous reporting

* 🧩 **Profiles (optional)**

  * Company-specific customization
  * Industry-specific extensions

---

## 🏗️ Repository Structure

```text
spec-kit-pm/
  templates/
    project/
    roadmap/
    risks/
    decisions/
    kpi/
  agents/
    pm.md
    reviewer.md
    risk-analyst.md
    reporter.md
  workflows/
    spec-to-plan.md
    execution-loop.md
  profiles/
    example-company/
  examples/
```

---

## ⚡ Get Started

### 1. Install the Specpm CLI

> **Status:** the `specpm` CLI is **planned** — see [Roadmap](#-roadmap). The commands in this section are the **specified UX** that will work once the CLI ships. Until then, use *Option 3: Manual setup* below.
>
> **Important:** the only official, maintained packages for spec-kit-pm are published from this GitHub repository. Always install directly from GitHub as shown below.

Choose your preferred installation method:

#### Option 1: Persistent installation (recommended)

Install once and use everywhere. Pin a specific release tag for stability (check [Releases](https://github.com/CassandraGargoyle/spec-kit-pm/releases) for the latest):

```bash
# Install a specific stable release (recommended — replace vX.Y.Z with the latest tag)
uv tool install specpm-cli --from git+https://github.com/CassandraGargoyle/spec-kit-pm.git@vX.Y.Z

# Or install latest from main (may include unreleased changes)
uv tool install specpm-cli --from git+https://github.com/CassandraGargoyle/spec-kit-pm.git

# Alternative: using pipx
pipx install git+https://github.com/CassandraGargoyle/spec-kit-pm.git@vX.Y.Z
pipx install git+https://github.com/CassandraGargoyle/spec-kit-pm.git
```

Verify the installed version:

```bash
specpm version
```

Use the tool:

```bash
# Create a new project
specpm init <PROJECT_NAME>

# Or initialize inside an existing repo
specpm init . --agent claude
# or
specpm init --here --agent claude

# Inspect detected agents and templates
specpm check
```

Upgrade:

```bash
uv tool install specpm-cli --force --from git+https://github.com/CassandraGargoyle/spec-kit-pm.git@vX.Y.Z
# pipx users:
pipx install --force git+https://github.com/CassandraGargoyle/spec-kit-pm.git@vX.Y.Z
```

#### Option 2: One-time usage

Run directly without installing:

```bash
# Create a new project (pinned to a stable release — replace vX.Y.Z with the latest tag)
uvx --from git+https://github.com/CassandraGargoyle/spec-kit-pm.git@vX.Y.Z specpm init <PROJECT_NAME>

# Or initialize in an existing project
uvx --from git+https://github.com/CassandraGargoyle/spec-kit-pm.git@vX.Y.Z specpm init . --agent claude
```

**Benefits of persistent installation:**

* Tool stays available in PATH
* No need for shell aliases
* Easier management with `uv tool list`, `uv tool upgrade`, `uv tool uninstall`

#### Option 3: Manual setup (works today)

While the CLI is in development, vendor the kit directly into your repo:

```bash
# As a git submodule (recommended — easy upstream sync)
git submodule add https://github.com/CassandraGargoyle/spec-kit-pm.git .pm-spec

# Or shallow clone if you don't want the submodule overhead
git clone --depth 1 https://github.com/CassandraGargoyle/spec-kit-pm.git .pm-spec

# Or simply copy the templates/, agents/, and workflows/ directories into your project
```

#### Option 4: Enterprise / air-gapped installation

For environments without access to PyPI or GitHub, build a portable wheel bundle on a connected machine using `pip download` against the `git+https://…` URL above and transfer it to the target host. (Detailed guide will land alongside the CLI release.)

---

### 2. Initiate the project (Initiation gate)

Every project MUST pass the **Initiation gate** before any planning artifact is produced. The gate produces a [Project Charter](templates/project/charter.md) at `specs/project/<project-id>/project.md` that records the source authority, a single named Project Manager, the Sponsor, and the artifact directory.

Use **`/specpm.init`** to draft the Charter against [`templates/project/charter.md`](templates/project/charter.md). The agent will refuse to skip this step — see [`agents/pm.md`](agents/pm.md) (preflight) and the [project-initiation workflow](workflows/project-initiation.md).

```text
/specpm.init Initiate project from contract examples/contracts/smart-home-installation-contract.md. Project Manager: Jane Doe <jane@acme.example>. Sponsor: Acme VP of Operations.
```

Result: `specs/project/<project-id>/project.md` with `status: active`. Only then may the iterative loop begin.

---

### 3. Establish project context

Use the **`/specpm.spec`** command in your AI agent to draft the project specification — context, goals, scope, constraints, success criteria. Focus on **why** and **what**, not on tasks.

```text
/specpm.spec Build a customer onboarding workflow for a B2B SaaS product. Primary goal is to cut time-to-first-value from 14 days to under 3 days. Constraints: must integrate with existing Salesforce CRM and HubSpot.
```

---

### 4. Generate the plan

Use **`/specpm.plan`** to turn the spec into an actionable plan — tasks, milestones, dependencies, owners.

```text
/specpm.plan
```

---

### 5. Identify risks and decisions

Use **`/specpm.risks`** to produce a risk register and **`/specpm.decisions`** to log architecture / approach decisions in ADR style.

```text
/specpm.risks
/specpm.decisions
```

---

### 6. Review

Use **`/specpm.review`** to have the reviewer agent check Charter, spec, plan, and risks for completeness, consistency, and unstated assumptions.

```text
/specpm.review
```

---

### 7. Report and iterate

Use **`/specpm.report`** to generate stakeholder-ready progress reports, then loop:

```text
[Initiation gate]  →  Spec  →  AI Plan  →  Execution  →  Validation  →  Update Spec
                       ▲                                                    │
                       └────────────────────────────────────────────────────┘
```

`Initiation` runs **once per project**; the iterative loop runs many times within an initiated project.

---

## 🧩 Profiles (Company Customization)

You can extend **spec-kit-pm** with company-specific profiles:

```text
profiles/
  infinite-solution/
    terminology.md
    roles.md
    approval-process.md
    kpi-model.md
    ai-policy.md
```

Use profiles to define:

* company terminology
* roles & responsibilities
* approval workflows
* KPI definitions
* AI usage policies

---

## 🔄 Upstream & Fork Model

Recommended setup:

```text
CassandraGargoyle/spec-kit-pm   # upstream (core)
InfiniteSolution/spec-kit-pm    # company fork
```

Keep your fork updated:

```bash
git remote add upstream https://github.com/CassandraGargoyle/spec-kit-pm.git
git fetch upstream
git rebase upstream/main
```

---

## 🧠 How It Fits in AI Projects

Traditional PM:

* task management
* manual planning
* meetings

spec-kit-pm:

* context definition
* AI-generated plans
* decision governance

👉 The PM becomes a **context architect and decision maker**

---

## 📈 Example Workflow

```text
0. Initiation gate — Charter signed off (once per project)
1. Define project spec
2. AI generates:
   - plan
   - risks
   - tasks
3. Team executes
4. AI reports progress
5. Update spec → loop back to 1
```

---

## ⚠️ Non-Goals

* ❌ Not a task management tool
* ❌ Not a replacement for Jira / Azure DevOps
* ❌ Not a rigid methodology

It is a **specification layer above your tools**.

---

## 🧭 Roadmap

* [ ] First template set (project spec, decision log, risk register)
* [ ] Initial AI agent instructions (PM, reviewer)
* [ ] `specpm` CLI — `uv tool install` / `pipx` / `uvx` install paths, `init` / `check` / `version` subcommands (see [Get Started](#-get-started))
* [ ] Slash-command bundles (`/specpm.spec`, `/specpm.plan`, `/specpm.risks`, `/specpm.review`, `/specpm.report`) for Claude Code, Copilot, and other agents
* [ ] Air-gapped install bundle (`pip download` recipe)
* [ ] AI-native validation pipelines
* [ ] Integration with [github/spec-kit](https://github.com/github/spec-kit) (dev companion)
* [ ] Multi-agent orchestration
* [ ] Synapse / Portunix integration

---

## 🤝 Contributing

Contributions are welcome:

* new templates
* improved workflows
* AI agent roles
* real-world examples

---

## 📄 License

[MIT](LICENSE) © 2026 CassandraGargoyle Team

---

## 💡 Vision

> Replace task-driven project management with **context-driven, AI-orchestrated execution**.
