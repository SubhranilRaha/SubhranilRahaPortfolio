# 0015: Scene construction

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-051

## Context
The spec describes one continuous camera path rising "up the stack" through six stations: terminal, toolchain, pipeline, cloud network, cluster, GPU racks. It must run on phones, hold 60 fps on desktop, load lazily, and stay within a mobile LCP target. The owner will generate still images but not 3D models. CLAUDE.md requires all text to be real HTML, never drawn in the canvas.

## Decision
Proposed during planning; confirmed or revised in T-051.

- **Geometry is procedural.** Stations are built in code from primitives, lines and instanced meshes. There are no model files and no image textures inside the scene.
- **No real-time shadows on any setting.** Depth comes from fog, light direction and colour.
- **One scene, one camera path.** All six stations exist in a single world. The camera follows one spline with a shot per chapter and holds its shot through the long pinned sections.
- **Colours are shared.** The scene reads the same tokens as the CSS, from the style bible.
- **No text and no brand marks in the scene.** Labels are HTML; vendor logos are not drawn.
- **A budget governs each station.** Draw calls, triangles and frame time are recorded in T-013 and checked in every station task.

## Alternatives considered
- Models made in Blender and loaded as glTF: richer shapes, but larger downloads, a modelling step the project has no one to do, and an asset pipeline to maintain.
- Baked lighting: good-looking and cheap at runtime, but it needs the modelling pipeline above.
- A separate scene per section with cross-fades: simpler per section, but it breaks the single journey the story depends on.
- Real-time shadows on desktop only: the spec forbids them only on mobile, but they cost frame time and create two looks to keep consistent.

## Consequences
- The look is limited to what procedural geometry does well. The three directions in T-003 are designed with that limit in mind.
- The scene adds almost nothing to download beyond the code itself.
- Every shape can be tuned in code, and the study and the app share the same construction.
- Richness in the foreground comes from the generated cutouts (decision 0002), not from the 3D.
