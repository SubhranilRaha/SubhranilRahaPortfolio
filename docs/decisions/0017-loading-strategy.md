# 0017: Loading strategy

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-065

## Context
The spec asks for a loader with real progress that shows content after 3 seconds at most. It also asks for a mobile LCP under 2.5 seconds, a Lighthouse mobile Performance score of at least 85, a lazy-loaded 3D bundle, and content that stays readable without the 3D. A loader that hides content for up to 3 seconds pulls against an LCP target of 2.5 seconds. This is the highest technical risk in the build.

## Decision
Proposed during planning; confirmed or revised in T-065.

- **Content first.** The hero heading and intro are in the server HTML and are not hidden while waiting for script. They can paint before anything else loads.
- **The loader is an overlay**, also in the server HTML, drawn above the content.
- **Progress is real.** It combines actual events: fonts ready, the three.js chunk loaded, the scene's first frame, the hero's cutout images loaded. The number never goes backward.
- **A 3-second cap.** At 3 seconds from the start of navigation the overlay lifts whatever has loaded; the rest continues underneath.
- **A CSS failsafe.** A pure CSS rule removes the overlay at 3 seconds, so a script failure cannot leave the page covered.
- **The three.js chunk is requested after first paint**, never as part of the initial script.
- **Reduced motion skips the loader.**

Two points are settled by measurement, not in advance: whether the static still sits under the canvas as a poster for every visitor (T-050), and whether the loader runs on every full load or once per session (open question 10).

## Alternatives considered
- A timed loader with invented progress: simpler, but the spec asks for real progress.
- Holding the page until WebGL is ready: the wait has no upper bound on a slow phone.
- No loader: the spec requires one, and it sets the tone for the story.

## Consequences
- LCP and the Lighthouse score are measured three times: a baseline at T-050, with the loader at T-065, and on the production URL at T-087.
- If the loader and the LCP target cannot both hold on a mid-range phone, a spec change is proposed to the owner; the loader is not quietly weakened.
- On repeat visits with a warm cache the loader clears almost at once.
- The loader's text comes from Sanity, so the overlay depends on the cached home-page data like everything else.
