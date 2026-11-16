# 0006: Fonts

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-017

## Context
CLAUDE.md asks for one display font for headings and one monospace font for labels, captions and commands, self-hosted through `next/font`. It does not say which font sets body text. The families themselves are chosen in decision 0004, where each direction proposes a pair.

## Decision
Proposed during planning; confirmed or revised in T-017.

- The two families are the pair from the direction chosen in decision 0004. Only open-licence fonts are candidates.
- Body text uses the display family at a text weight unless the style bible (T-003) says otherwise.
- Files are variable WOFF2, Latin subset, loaded with `next/font/local` from `src/app/fonts/`. They are the same files the studies use, so the app matches what was approved.
- The display font is preloaded. The monospace font is preloaded only if it appears above the fold.
- Fallback metrics are adjusted so text does not shift when the fonts arrive.
- Licence files are committed next to the fonts.

## Alternatives considered
- `next/font/google`: also self-hosts, with no files in the repo, but downloads from Google at build time and can differ from the files used in the studies.
- System fonts: no download, but no control over the look across devices.
- A font CDN: not allowed by CLAUDE.md.

## Consequences
- Font files and licences live in the repo; updating a font is a manual step.
- The share image generator (T-083) needs the display font in a format it accepts, which may mean one extra file. This is checked in T-083.
- Layout shift from fonts is measured in T-017 and must be zero.
