# 0016: Adaptive quality

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-060

## Context
Commit `8b9edf5` changed the spec from "no WebGL below 768 px" to the same experience on phones at adaptive quality: pixel ratio capped at 1.5, about 40 % of the particles, lighter post-processing, no real-time shadows. A performance monitor steps quality down and falls back to the static scene image only if the device cannot hold 30 fps. Reduced-motion visitors always get the static image.

## Decision
Proposed during planning; confirmed or revised in T-060.

- **Four settings:** High, Mobile, Low and Static. The table is in `docs/architecture.md`; the Low values are fixed in T-060.
- **Starting point.** Mouse-driven devices with a wide viewport start at High. Touch devices start at Mobile. A low core count starts one step lower.
- **Measuring.** drei's performance monitor watches the real frame rate. Quality steps down one setting at a time, with a margin so it does not flip back and forth.
- **Falling back.** Static is chosen only after the frame rate stays under 30 fps at Low. The canvas fades out over the static image with no flash and no change in scroll position.
- **Stepping up** happens at most once per visit, after a sustained good period.
- **Remembering.** The result is kept for the browser session, so a reload does not repeat the test.
- **Applying.** Pixel ratio and particle count change without remounting the canvas.
- **Reduced motion** selects Static immediately and never creates a canvas.

## Alternatives considered
- `detect-gpu`: guesses the device class from a benchmark list, but it fetches that list at runtime and the data ages.
- Fixed breakpoints by screen width: the spec's earlier approach, removed on purpose; screen size says little about GPU strength.
- Pixel-ratio scaling only: helps fill-rate problems, not a device that is too slow overall.
- No adaptation: fails the spec.

## Consequences
- Two visitors on similar phones can see different quality. That is intended.
- The starting rules are guesses; the monitor corrects them. The thresholds need tuning on the owner's test phone (open question 8).
- Under Lighthouse's CPU throttling the scene will likely fall back to Static, which helps the score and must not hide a real problem; T-087 also measures on a real phone.
- The static image must be ready before any fallback can happen (T-064).
