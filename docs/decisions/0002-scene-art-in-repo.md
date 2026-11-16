# 0002: Scene art lives in the repo

- **Status:** Accepted
- **Date:** 2026-11-16
- **Task:** T-001

## Context
CLAUDE.md says all images come from Sanity through the image URL builder. Scene art is a different kind of image from content: the foreground cutouts pinned over the canvas, and the static scene image shown to reduced-motion visitors and to devices that fall back. Each piece has a fixed slot, size and parallax set in code, and the Phase A studies need the files locally before the app exists.

## Decision
Chosen by the owner on 2026-11-16.

Scene art lives in `public/scene/` and is served through `next/image`. A script (T-062) converts the owner's originals to WebP at the sizes in the asset brief, and a typed manifest (`src/components/scene/art.ts`) lists each slot. Only optimized files are committed; originals are git-ignored.

Every content image (projects, certifications, posts) stays in Sanity under decision 0011.

## Alternatives considered
- A "scene art" document in Sanity with one named image slot per piece: follows the rule literally and allows swapping art without a deploy, but a replacement with a different shape can break a composition, it adds a schema type, and first paint would depend on Sanity.

## Consequences
- Replacing a piece of scene art means a commit and a deploy. The runbook (T-094) explains how.
- The art is versioned together with the code that positions it.
- CLAUDE.md's image rule needs wording for this exception (T-001).
- These few local images go through Vercel's image optimizer. That is small against the 5,000 transformations a month on the Hobby plan.
- Cutouts are decorative and carry empty alt text; the required-alt rule applies to content images.
