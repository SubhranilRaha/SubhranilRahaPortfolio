# 0003: Project detail is an overlay dialog

- **Status:** Accepted
- **Date:** 2026-11-16
- **Task:** T-001

## Context
The spec says clicking a project card "opens a detail view with summary, tech, links and the gallery (keyboard and swipe navigable lightbox)". It does not say whether that view is an overlay on the home page or has its own URL.

## Decision
Chosen by the owner on 2026-11-16.

The detail view is an overlay built on the native `<dialog>` element, opened from the card. It can be linked directly as `/#project-<slug>`, and it closes on Esc and on the browser's Back button. The gallery inside it uses the shared lightbox (T-041).

## Alternatives considered
- A page per project plus an overlay through an intercepting route: gives each project its own URL, metadata and share image, but costs about four more tasks and makes scroll restoration around the pinned sections harder.
- A dialog library: adds a dependency for behaviour the native element already provides (focus containment, Esc, top layer).
- A page only, no overlay: breaks the single continuous scroll the story depends on.

## Consequences
- A project has no separate URL or share preview in v1. Adding pages later needs a new record.
- The home page carries the detail content for every project; gallery images load lazily.
- While the dialog is open the page behind must not scroll, and smooth scrolling must pause (T-042, T-049).
- The pinned deployment track keeps its position when the dialog closes (T-071).
