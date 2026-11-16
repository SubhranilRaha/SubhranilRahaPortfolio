# Progress log

> Updated at the end of every session. Newest entry first.

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
