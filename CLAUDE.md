# The Continent (fork of Abyssal Garden)

A fantasy continent you can walk through in the browser, built region by region with Abyssal Garden's technique: WebGPU, no engine, everything procedural, one HTML file per region. Engine conventions: `.claude/skills/webgpu-world/SKILL.md`. World bible: `world/` (map, overview, regions, races, creatures).

## Planning: Jira
- Site: brechtvandenbroeck8.atlassian.net, Kanban project **WORLD** (key to be confirmed once the user creates it).
- **Epic** = a region or a cross-cutting engine capability (e.g. "Flauma & the western ranges", "Engine: walking on terrain").
- **Story** = one buildable, viewable slice ("Flauma: coastal mountain range terrain", "Silent Lake water"). Each story names its region spec section and has acceptance criteria the user can check by walking through it.
- **Task** = engine or tooling work that isn't directly visible.
- Board columns: To Do → Design → Build → Review → Done. The master moves cards; the user moves cards into Done after walking through the build.

## How we work: one master chat per region epic
The master plans, talks with the user, updates Jira and `world/`, and delegates to the agents in `.claude/agents/`. It doesn't write engine code itself. **Jira and `world/` are the memory, not the chat.**

### Starting or resuming an epic
1. Ask which epic this is. Read its Jira epic and `world/regions/<region>.md`.
2. If `region/<name>` doesn't exist, create it from `main` and push it.

### For each story
1. Ideate with the user (via `world-designer`) until the spec section is agreed. Move the card to *Design*.
2. `world-designer`: build spec with 6 fixed viewpoints. **The user approves it.**
3. Branch `feature/<JIRA-KEY>-<short-name>` from `region/<name>`. Move the card to *Build*.
4. `world-dev`: builds, screenshots, benchmarks.
5. `visual-critic`: judges screenshots only. Send blockers/majors back to `world-dev`; loop until PASS.
6. Show the user the screenshots and the playable build (published as an Artifact or the HTML file). Move the card to *Review*.
7. `reviewer`: review; if clean, commits, opens a PR and merges it into `region/<name>`. Comment the PR link on the Jira story.
8. The user walks through it and moves the card to *Done*.

### Ending an epic
Ask the user before opening the PR `region/<name>` → `main`. **Only the user merges into `main`.**

## Rules
- Work step by step: after each step, show the result and wait for the user.
- The user is the play-tester and the author of the world. Never invent lore silently; mark proposals.
- Nobody pushes to `main` or force-pushes.
