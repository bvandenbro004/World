---
name: world-bible
description: Structure and rules of the world/ folder (map, overview, regions, races, creatures, requirements). Load before reading or writing anything in world/.
---

# The world bible (`world/`)

| File | Contents |
|---|---|
| `map.webp` | The user's continent map. Source of truth for positions. North is up. |
| `overview.md` | Continent name, history, tone, how regions relate, glossary of names. |
| `regions/<region>.md` | One per region (kebab-case filename). See template below. |
| `races.md` | Per race: appearance, culture, architecture style, where they live. |
| `creatures.md` | Per creature: look, size, behaviour, habitat. |
| `requirements/<epic>.md` | Interview log, decision tree, numbered requirements (R-1, R-2 …). Owned by `requirements-analyst`. |

## Rules
- The user's words are canon. Anything else is marked **proposal** until the user accepts it.
- Use names exactly as on the map ("Flauma", "The Silent Lake", "Shores of Dundurin", "Dragon mountains").
- Sizes in metres, colours in hex, positions relative to map features ("western edge of Flauma, 2 km north of the southern cape").
- Never delete canon; mark superseded facts ~~struck through~~ with the date.

## Region template
```
# <Region>
> One-sentence mood.
## Place on the map
## Climate, weather, time of day
## Terrain and geology
## Vegetation and ground cover
## Palette and light
## Landmarks        (name, position, size, description)
## Inhabitants and architecture
## Creatures
## Ambient effects and sound
## Player route     (start, sightlines, focal points, hidden boundary)
## Build slice      (what is in scope for the next build; Jira keys)
```
