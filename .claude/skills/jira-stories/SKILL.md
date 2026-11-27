---
name: jira-stories
description: How this project's Jira is set up and how to write and file epics, stories and tasks for the fantasy-continent project. Load before creating, updating or moving any Jira issue.
---

# Jira for the continent

- Site cloudId: `e20a4b23-9d9e-445c-8b52-41ff65bde180` (brechtvandenbroeck8.atlassian.net)
- Project: **WORLD** ("Magical-World", team-managed Kanban). Types: Epic, Story, Task, Bug, Feature, Subtask.
- Statuses: To Do → In Progress → In Review → Done. Only the user moves an issue to Done.
- Tools: `createJiraIssue`, `editJiraIssue`, `transitionJiraIssue`, `addOrEditJiraIssueComment`, `searchJiraIssuesUsingJql` (Atlassian MCP). Search before creating to avoid duplicates.

## Types
- **Epic**: a region ("Flauma & the western ranges") or an engine capability ("Engine: walking on terrain"). Description: one-paragraph vision, link to `world/requirements/<epic>.md` and `world/regions/<region>.md`, scope / out of scope.
- **Story**: one slice the user can walk through and judge. Parent = its epic.
- **Task**: engine or tooling work with no direct visible result.
- **Bug**: something built that is wrong vs. its story or broken.

## Story template
Summary: `<Region>: <what you can see/do>` (e.g. "Flauma: snow-capped coastal ridge at dusk").

Description (markdown):
```
**As** a traveller in <region>, **I want** <experience>, **so that** <feeling/purpose>.

**Spec:** world/regions/<region>.md § <section>
**Requirement refs:** R-<n>, R-<n> (world/requirements/<epic>.md)

**Acceptance criteria** (checked by the user walking through the build)
- [ ] From viewpoint <n> I can see …
- [ ] Walking from … to … I …
- [ ] Runs at ≥ 60 fps on High on the user's PC; loads on Low on a phone

**Out of scope:** …
```
Labels: region name in kebab-case (e.g. `flauma`), plus `engine`, `terrain`, `vegetation`, `set-piece`, `creatures`, `sky`, `water`, `audio`, `controls` as fits.

Keep stories small: something buildable and reviewable in one feature branch.
