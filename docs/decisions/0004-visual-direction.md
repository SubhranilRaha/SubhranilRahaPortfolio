# 0004: Visual direction

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-010

## Context
CLAUDE.md fixes the family the design must stay inside: ink-slate background, off-white text, one amber accent, muted steel for secondary; one display font and one monospace font; restraint. It does not fix the exact colours, the fonts, the scene's materials and lighting, or the composition. The owner asked for these to be settled early, through standalone studies, before any app code.

## Decision
Not made yet. This record is completed in T-010.

The process is decided:
1. T-003 defines three directions (A, B, C) in `docs/design/style-bible.md`. They must differ in field colour, material, light behaviour, type pairing and composition, not only in accent colour.
2. T-005 to T-009 build each direction as one HTML study covering the loader, the hero and the first camera move.
3. In T-010 the owner views all three on desktop and on a phone and picks one or a mix. This record then names the choice, and the style bible is reduced to one final token table.

## Alternatives considered
- The two directions not chosen: recorded here in T-010, with the reason.
- Designing directly in the app without studies: iteration is slower inside a build, and the direction would be settled late.

## Consequences
- T-011 (asset brief), T-012 and T-013 (master study), T-017 (tokens and fonts) and T-051 (scene base) all depend on this choice.
- The chosen fonts become decision 0006.
- Whether the scene needs post-processing follows from the chosen direction and decides whether T-061 runs.
- The do-not-copy list from T-002 applies to all three directions.
