# Gantt Chart — Specification & Template

## Convention

Gantt charts in this project **must** be authored in [Mermaid](https://mermaid.js.org/) using the [`gantt`](https://mermaid.js.org/syntax/gantt.html) diagram type.

**Why Mermaid:**

- Plain-text, diff-friendly, reviewable in pull requests
- Renders natively in GitHub, GitLab, and most Markdown viewers
- AI agents can generate, read, and update it without binary tooling
- No external image files or proprietary editors required

**Do not** use:

- Image exports from MS Project, ProjectLibre, GanttProject, or similar
- Screenshots of spreadsheet timelines
- Embedded binary diagrams

## Required Elements

Every Gantt chart in this repository should include:

1. `title` — what the timeline represents
2. `dateFormat` — explicit, ISO-style (`YYYY-MM-DD`) preferred
3. At least one `section` grouping related tasks
4. Stable task IDs for tasks referenced by `after` dependencies
5. Status markers (`done`, `active`, `crit`) where applicable

## Template

````markdown
```mermaid
gantt
    title <Project / Milestone Title>
    dateFormat YYYY-MM-DD
    axisFormat %Y-%m

    section <Phase 1 Name>
    <Task A>            :a1, 2026-01-01, 14d
    <Task B>            :a2, after a1, 10d

    section <Phase 2 Name>
    <Task C> (critical) :crit, c1, after a2, 21d
    <Task D>            :active, c2, 2026-03-01, 30d
    <Task E> (done)     :done, c3, 2026-02-01, 2026-02-15
```
````

## Rendered Example

```mermaid
gantt
    title spec-kit-pm — Initial Roadmap
    dateFormat YYYY-MM-DD
    axisFormat %Y-%m

    section Foundations
    Repository structure       :done,    f1, 2026-04-30, 1d
    First template set         :active,  f2, after f1, 21d

    section Agents & Workflows
    PM & reviewer agents       :         a1, after f2, 14d
    Spec → Plan workflow       :         a2, after a1, 14d

    section Tooling
    CLI scaffold               :         t1, after a2, 21d
    Validation pipelines       :crit,    t2, after t1, 30d
```

## References

- Mermaid project: <https://mermaid.js.org/>
- Gantt syntax reference: <https://mermaid.js.org/syntax/gantt.html>
- Live editor: <https://mermaid.live/>
