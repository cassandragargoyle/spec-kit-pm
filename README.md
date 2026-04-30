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

## ⚙️ Getting Started

### 1. Initialize in your project

```bash
# copy or clone into your repository
git submodule add https://github.com/CassandraGargoyle/spec-kit-pm.git .pm-spec
```

Or manually copy templates into your project.

---

### 2. Create your first project spec

```text
specs/project/my-project.md
```

Start with:

* context
* goals
* scope
* constraints

---

### 3. Let AI generate the plan

Use your preferred AI tool (e.g., Claude Code, Copilot, etc.):

* Generate tasks
* Identify risks
* Propose architecture decisions
* Suggest KPIs

---

### 4. Execute & iterate

Loop:

```text
Spec → AI Plan → Execution → Validation → Update Spec
```

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
1. Define project spec
2. AI generates:
   - plan
   - risks
   - tasks
3. Team executes
4. AI reports progress
5. Update spec
```

---

## ⚠️ Non-Goals

* ❌ Not a task management tool
* ❌ Not a replacement for Jira / Azure DevOps
* ❌ Not a rigid methodology

It is a **specification layer above your tools**.

---

## 🧭 Roadmap

* [ ] CLI tooling
* [ ] AI-native validation pipelines
* [ ] Integration with spec-kit (dev)
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
