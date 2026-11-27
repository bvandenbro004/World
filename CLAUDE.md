# The Continent (fork of Abyssal Garden)

A fantasy continent you can walk through in the browser, built region by region with Abyssal Garden's technique: WebGPU, no engine, everything procedural, one HTML file per region. Engine conventions: `.claude/skills/webgpu-world/SKILL.md`. World bible: `world/` (map, overview, regions, races, creatures).

## Planning: Jira
- Site: brechtvandenbroeck8.atlassian.net, Kanban project **WORLD** ("Magical-World"). Conventions: `.claude/skills/jira-stories/SKILL.md`.
- **Epic** = a region or a cross-cutting engine capability (e.g. "Flauma & the western ranges", "Engine: walking on terrain").
- **Story** = one buildable, viewable slice ("Flauma: coastal mountain range terrain", "Silent Lake water"). Each story names its region spec section and has acceptance criteria the user can check by walking through it.
- **Task** = engine or tooling work that isn't directly visible.
- Board columns: To Do → In Progress → In Review → Done. The master moves cards; the user moves cards into Done after walking through the build.

## How we work: one master chat per region epic
The master plans, talks with the user, updates Jira and `world/`, and delegates to the agents in `.claude/agents/`. It doesn't write engine code itself. **Jira and `world/` are the memory, not the chat.**

### Starting or resuming an epic
1. Ask which epic this is. Read its Jira epic, `world/requirements/<epic>.md` and `world/regions/<region>.md`.
2. If `region/<name>` doesn't exist, create it from `main` and push it.

### Requirements first (every new epic, and any big new idea)
1. `requirements-analyst` runs the `grill-me` interview: it returns a few questions at a time, the master asks the user, and feeds the answers back. The log lives in `world/requirements/<epic>.md`, so the interview can span many chats.
2. When every branch is decided or parked, it writes the requirements and drafts the epic and stories. **The user approves the draft**, then it creates them in Jira.

### For each story
1. `world-designer`: region spec section and build spec with 6 fixed viewpoints, from the requirements. **The user approves it.**
2. Branch `feature/<JIRA-KEY>-<short-name>` from `region/<name>`. Move the card to *In Progress*.
3. `world-dev`: builds, screenshots, benchmarks.
4. `visual-critic`: judges screenshots only. Send blockers/majors back to `world-dev`; loop until PASS.
5. Show the user the screenshots and the playable build (published as an Artifact or the HTML file).
6. `reviewer`: review; if clean, commits, opens a PR, merges it into `region/<name>`, comments the PR link on the story and moves it to *In Review*.
7. The user walks through it and moves the card to *Done*.

### Ending an epic
Ask the user before opening the PR `region/<name>` → `main`. **Only the user merges into `main`.**

## Rules
- Work step by step: after each step, show the result and wait for the user.
- The user is the play-tester and the author of the world. Never invent lore silently; mark proposals.
- Nobody pushes to `main` or force-pushes.
