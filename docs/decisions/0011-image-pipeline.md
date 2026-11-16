# 0011: Image pipeline for content images

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-029

## Context
CLAUDE.md requires content images to come from Sanity through the image URL builder, with responsive sizes, WebP or AVIF, a blur placeholder, required alt text, and lazy loading below the fold. Every image field has a crop hotspot. Vercel's Hobby plan includes 5,000 image transformations a month.

Checked on 2026-11-16: next-sanity ships an `Image` component and loader at `next-sanity/image` that send requests straight to Sanity's image CDN, but its docs mark that API as alpha.

Scene art is outside this record (decision 0002).

## Decision
Proposed during planning; confirmed or revised in T-029.

- One component, `SanityImage`, wraps `next/image` with a small custom loader built on `@sanity/image-url`.
- The loader requests each width directly from Sanity's CDN with `auto=format`, a quality value, and the crop and hotspot from the field. Vercel's optimizer is not involved.
- Queries fetch the asset's blur placeholder and dimensions with the image. The placeholder shows while the image loads; the dimensions reserve the space so nothing shifts.
- `alt` is a required prop, filled from the field.
- Each use sets `sizes` for its layout. Images load lazily unless they are above the fold.

## Alternatives considered
- `Image` from `next-sanity/image`: does much the same with less code, but the API is alpha and may change.
- Next's default optimizer with Sanity added as a remote source: every image is processed twice and spends the Hobby plan's transformations.
- Plain `<img srcset>`: full control, but the lazy loading, sizing and placeholder behaviour would all be written by hand.

## Consequences
- Content images cost no Vercel transformations.
- Image delivery depends on Sanity's CDN being up; a failed image must not break its card.
- A crop at a new aspect ratio needs both width and height passed, so the hotspot is respected.
- If `next-sanity/image` becomes stable, switching is a small change behind `SanityImage`.
