# 0012: List layouts first, scroll patterns on top

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-033

## Context
Four sections have a reserved scroll pattern: Experience (pinned commit graph), Projects (pinned horizontal track), Writing (stacked cards), Certifications (checks panel). The spec also requires that reduced-motion visitors get plain list layouts with the same content, that all content stays readable with the 3D disabled, and that everything is keyboard navigable. CLAUDE.md asks for Server Components by default and real HTML text.

The owner's phases follow the same split: Phase D builds each section with its mobile and reduced-motion behaviour; Phase E adds the four patterns.

## Decision
Proposed during planning; confirmed or revised in T-033.

- Each section has one server-rendered list layout that is complete on its own: an ordered list for Experience, a grid for Projects, a card list for Writing, the checks panel for Certifications. This is what reduced-motion visitors and visitors without JavaScript get.
- A scroll pattern is a client component that enhances that same markup. It mounts only when the visitor allows motion. There is one copy of the content, never two.
- The scene follows the same rule: the static scene image is the base, the canvas is the enhancement.
- The list is the accessible structure. Decorative drawings such as the commit graph are hidden from screen readers.
- Nothing is reachable only by scroll position. Tabbing to an item that is off screen in a pinned section brings it into view.
- One shared hook reports the motion preference to components; CSS-only motion is guarded by the matching media query.

## Alternatives considered
- Two separate component trees per section, one static and one animated: duplicated markup that drifts apart.
- Client-only animated sections: fails the no-JavaScript and reduced-motion requirements and ships more script.
- CSS scroll-driven animations alone: no script, but pinning with correct spacing is not covered and browser support has to be checked.

## Consequences
- The site at the end of Phase D is complete and shippable without Phase E.
- The list markup constrains each pattern: the pattern must be achievable by pinning and transforming elements that already exist.
- Pinning lengthens the page after the script loads. The patterned sections are below the fold, anchors are recalculated after mount, and layout shift is checked in every Phase E task.
