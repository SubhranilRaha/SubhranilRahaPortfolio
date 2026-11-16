# 0009: Content model

- **Status:** Proposed
- **Date:** 2026-11-16
- **Task:** T-023

## Context
CLAUDE.md forbids hard-coded copy, dates and links in components; the only exception is fixed interface text such as button labels and aria text. `content.md` holds more than the spec's list of editable types: per-chapter labels and captions, hero copy, section intros, contact text, a footer line, a loader line and a 404 caption. Certification dates come in several shapes ("Nov 2026", "2026", "Expected Dec 2026"). Each experience entry shows a short fake commit hash and a commit-style title.

## Decision
Proposed during planning; confirmed or revised in T-023.

- **Two single documents.** `siteSettings` holds identity: name, title line, location, public email, social links, the resume PDF and SEO fields. `homePage` holds the copy of every chapter in tabs: label, heading, intro and an optional caption, plus hero copy, About text and quick facts, contact copy, the footer line, the loader line and the 404 caption.
- **Six collections.** `skillGroup`, `experience`, `project`, `post`, `certification`, `milestone`.
- **Shared field types.** `imageWithAlt` (image, crop hotspot, required alt text), `richText`, `seo`, `chapterCopy`.
- **Chapter order and ids live in code** (`src/lib/chapters.ts`); chapter copy lives in Sanity. Nav labels come from the chapter headings.
- **Button labels and aria text stay in code**, as CLAUDE.md allows.
- **Ordering.** Skills, projects and milestones have a manual order. Experience and posts sort by date.
- **Certification dates** are stored as a display label plus a sort date, so "Expected Dec 2026" and "2026" both work.
- **Experience.** The commit title is a field. The short hash is derived from the document id, so it is stable and needs no input. Which branch a role sits on follows from its type.
- **Resume.** A PDF file on `siteSettings`, reached through `/resume`, which redirects to the current file.
- **Captions are always optional**, and a missing caption renders nothing.

## Alternatives considered
- One document per chapter: flexible, but nine near-identical documents for one page and more clicking for the editor.
- Everything in one document: simple to query, but one long form and no per-item publishing for projects or certifications.
- Chapter labels in code: fewer fields, but it breaks the no-hard-coded-copy rule.
- A single date field for certifications: cannot express a year alone or an expected date.

## Consequences
- The editor works in two places for copy and six lists for items; the runbook (T-094) maps each part of the page to its place in Studio.
- Generated types mark most fields optional, so every component handles missing values, including a project without a cover.
- Section headings beyond Hero and Contact are not in `content.md`; where they come from is open question 5. Commit titles are open question 3.
- Adding a chapter needs a code change (order and id) as well as content.
