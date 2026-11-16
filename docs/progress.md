# Progress log

> Updated at the end of every session. Newest entry first.

## 2026-11-16 (third session: open questions answered)
- Done: the owner's answers to open questions 1 to 12 are recorded in `docs/tasks/TASKS.md`. Each question keeps its number and the task it blocked. No task was started, no app code written, nothing committed.
- What changed in the tasks:
  - New T-096: draft the five commit-style titles and the Writing final-card wording, get the owner's approval, then add them to `content.md`. T-030 and T-031 now wait for it.
  - T-001 now also applies the answers to the spec, `content.md` and `docs/architecture.md`, and writes decision 0021 (posts carry a source, Hashnode or LinkedIn), which supersedes 0001.
  - Writing and posts: T-023, T-025, T-043, T-073 (source label, final card for both sources, one to three posts).
  - Content import: T-030, T-031, T-033 (section headings seeded from the spec's names, EY with one highlight, T-033 now needs the import).
  - Footer: T-048, T-076, T-078 ("visits" as a running total, computed copyright).
  - Loader: T-065 (every full load, one named setting, LCP measured on first and repeat loads, stop and ask if it fails).
  - Phone checks: T-010, T-013, T-041, T-049, T-050, T-060, T-067, T-070, T-072, T-087, T-089, T-095 (iPhone only, Android marked emulation only).
  - Launch: T-018, T-080, T-092 (run on `*.vercel.app` first, buy the domain at T-092), and T-090 and T-095 (blocked on the `[FILL]` values).
  - Additions kept: T-016, T-019, T-034, T-090.
- Open: new question 13 (does the footer post count include LinkedIn posts, or Hashnode only), which blocks T-078 and one line of T-001.
- Still uncommitted: this session's edits to `docs/tasks/TASKS.md` and `docs/progress.md`. The plan itself is already committed (`9baf9e2`).
- Next: T-001. Its plan shows the exact wording for approval first.
- Waiting on the owner: question 13; approval of the drafts in T-096; the `[FILL]` values (14 left, 13 if the Hashnode host line is merged); the iPhone model and iOS version at T-010.

## 2026-11-16 (second session: build plan)
- Done: the full build plan is in the repo.
  - `docs/tasks/TASKS.md`: 95 tasks (T-001 to T-095) in nine groups, each with files, dependencies and a "Done when" check, plus 12 open questions
  - `docs/decisions/`: 20 records. 0001 to 0003 are Accepted (decided with the owner); 0004 to 0020 are Proposed and get confirmed in the task each one names
  - `docs/architecture.md`: the planned design and the risk list
- Decided with the owner:
  - Writing comes from post cards in Sanity, because Hashnode's GraphQL API became paid on 2026-05-13 (0001)
  - Scene art lives in the repo, content images in Sanity (0002)
  - Project detail is an overlay dialog, not a page (0003)
  - The `Read(./.env.*)` deny rule will be narrowed in T-016 so `.env.example` can be read
- Found while planning:
  - `typescript@latest` is 7, which the lint tooling does not support yet, so the plan pins 6.0.x; React is held at 19.3.x for react-three-fiber
  - pnpm, the Vercel CLI and `gh` are not installed on this machine
  - The phone notes in `content.md` predate commit `8b9edf5`; the plan follows the spec (same experience on phones)
- Half-finished: nothing. No task has started and no app code exists.
  - The spec, CLAUDE.md and the notes in `content.md` still describe the Hashnode API and the old phone behaviour; T-001 corrects them
  - This session's files were left uncommitted
- Next: answer the open questions in `TASKS.md` (4, 8 and 9 affect the earliest work), then start T-001
- Waiting on the owner: approval to install pnpm (T-014), the deny-rule change (T-016), the Vercel import (T-018), the Sanity project (T-020)

## 2026-11-16
- Done: content.md, design skills, project foundations (CLAUDE.md, spec, templates)
- Next: plan the whole build in plan mode; fill TASKS.md and the first decision records
