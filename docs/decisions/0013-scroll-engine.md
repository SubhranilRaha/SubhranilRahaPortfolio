# 0013: Scroll engine: Lenis with GSAP ScrollTrigger

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-049

## Context
One scroll position has to drive three things in step: the camera path through the scene, three pinned sections, and section reveals. The spec asks for the same patterns on phones, no scroll jumps when the mobile address bar resizes, and native behaviour under reduced motion. CLAUDE.md names GSAP ScrollTrigger and Lenis in the stack; this record gives the reasons and the rules for using them.

Checked on 2026-11-16: gsap is at 3.15 under its "Standard no charge" licence, lenis at 1.3 under MIT, and `@gsap/react` provides a hook that cleans up animations with the component.

## Decision
Proposed during planning; confirmed or revised in T-049.

- Lenis smooths wheel scrolling on desktop and runs on GSAP's ticker, so both stay on one clock. Touch devices keep native touch scrolling.
- Under reduced motion Lenis is never created and no ScrollTrigger pins are set.
- GSAP is registered once in `src/lib/motion.ts`. Components create animations through the `@gsap/react` hook so they are removed on unmount.
- There is one conductor: a ScrollTrigger per chapter writes the current chapter and its local progress into `src/lib/scrollStore.ts`. The scene reads that store every frame. Nothing else listens to scroll.
- The document keeps native, reversible scrolling. The wheel is never hijacked.
- ScrollTrigger ignores the resize caused by the mobile address bar, and positions are refreshed after fonts and images load.
- Lenis pauses while a dialog, the lightbox or the mobile menu is open. Neither library loads on `/studio`.

## Alternatives considered
- CSS scroll-driven animations: no script, but pinning with spacing and driving a WebGL camera still need script, and support has to be checked per browser.
- Motion's scroll hooks: capable, but the pinned horizontal track and pin spacing would be built by hand.
- drei's `ScrollControls`: moves the page into its own scroll container, which conflicts with native sections, anchors and accessibility.
- Plain scroll listeners: workable for the camera, a lot of code for the pinned patterns.

## Consequences
- Two libraries are added to the client bundle of the site layout; they are needed before the scene, so they are not lazy-loaded with it.
- Pinned sections on iOS Safari are the riskiest part of the build; each has a real-phone check.
- GSAP's licence terms are read once in T-049 and noted here.
- Anchor links and the `#project-<slug>` deep link must go through Lenis so they land correctly.
