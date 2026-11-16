# 0014: 3D runtime: react-three-fiber as host, three.js factories for geometry

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-050

## Context
The scene is first built in plain three.js as a standalone study (T-005 to T-013), then moved into the Next.js app. In the app it needs a managed lifecycle: lazy loading, resize, pausing when hidden, a performance monitor, cleanup on unmount, and a fallback when WebGL fails. CLAUDE.md names three.js through react-three-fiber and drei.

Checked on 2026-11-16: `@react-three/fiber` 9.8 requires React 19 below 19.4, drei 10.7 requires fiber 9, three is at 0.187.

## Decision
Proposed during planning; confirmed or revised in T-050.

- react-three-fiber hosts the scene: one canvas in a client component, loaded after first paint, fixed behind the HTML and hidden from assistive technology.
- drei supplies the performance monitor and a few helpers. Only what is used is imported.
- Each station's geometry is built by a plain three.js factory function that returns a group, mounted into the React tree. The study's code moves over almost unchanged.
- Each factory also returns a dispose function, because objects mounted this way are not cleaned up automatically. This is confirmed in T-053.
- The camera and anything that moves every frame are updated in the render loop from the scroll store, never through React state.
- An error boundary around the canvas swaps in the static scene image if WebGL fails.

The boundary between the two styles: React components own lifecycle, loading and quality settings; factories own geometry and materials.

## Alternatives considered
- Plain three.js in one client component: a smaller bundle, but resize, the render loop, loading, monitoring and cleanup would all be written by hand.
- Fully declarative JSX for every mesh: more idiomatic React, but instanced and procedural geometry reads better as plain code, and the port from the study would be a rewrite.
- An embedded 3D tool: a heavy runtime and little control over quality settings.
- Scrubbed video: not interactive, large files, and no way to adapt to the device.

## Consequences
- React stays below 19.4 until react-three-fiber allows it (decision 0005).
- three, fiber and drei load together as one lazy chunk; its size is watched from T-050.
- The study must be written with the port in mind: geometry in functions, colours and camera shots as data.
