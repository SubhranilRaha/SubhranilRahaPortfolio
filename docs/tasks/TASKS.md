# Tasks

> Task IDs are permanent (T-001, T-002 …). Each task has a "Done when" check.
> Filled in during planning on 2026-11-16. Open questions 1 to 12 were answered by the owner on 2026-11-16. Newly discovered work is added at the bottom of To do.
> The design is in `docs/architecture.md`; the reasons are in `docs/decisions/`.

## How every task runs

- **One task at a time.** A short plan for the task is posted, the owner approves, then it is built (CLAUDE.md rule 1). Each task starts by reading current docs for the libraries it touches, because several are newer than the planning notes.
- **Finishing a task** means `pnpm lint`, `pnpm typecheck` and `pnpm build` pass, the page is checked in the browser at 375 px and 1440 px, this file is updated, and there is one commit `T-0NN: description`. Phase A has no build; its check is opening the study or document.
- **3D and animation tasks add:** steady 60 fps on desktop (measured), no layout shift, the reduced-motion path works, the `optimize-web-animations` checks (nothing runs off screen or in a hidden tab), and a check on the owner's iPhone (iOS Safari, over Wi-Fi at `http://<mac-ip>:3000`, or the Vercel URL). "The phone" in this file means that iPhone. There is no Android device (answer 8): Android is covered by browser emulation only, and every Android row in a matrix or audit reads "emulation only, not tested on real hardware", never "pass".
- **Size.** Each task targets under 300 changed lines, not counting vendored libraries, lockfiles, generated types or images. Variants B and C start as copies of A, so their review unit is the diff against A.
- **Decisions.** Records 0001 to 0003 are Accepted. Records 0004 to 0020 are Proposed. A task with a "Confirms" line re-checks that record against current docs and sets it to Accepted. A Proposed record may be revised until then; once Accepted, a change needs a new record that supersedes it.
- **Scope.** Work discovered along the way becomes a new task at the bottom of To do.
- **"You:"** marks something only the owner can do: accounts, secrets, DNS, art, phone.
- **Terms.** A *chapter* is a page section (00 to 08). A *station* is one of the six stops in the 3D scene: terminal, toolchain, pipeline, cloud network, cluster, GPU racks.

## Phases

| Phase | Tasks | What exists at the end |
|---|---|---|
| Before A | T-001 | Spec, CLAUDE.md, content notes and architecture match decisions 0001 to 0003 and the recorded answers |
| A Design study | T-002 to T-013 | Three studies, a chosen direction, an asset brief, a full-path master study |
| B Scaffold | T-014 to T-019 | Empty typed app deployed on Vercel |
| C CMS | T-020 to T-032 | Studio at `/studio`, content imported, typed queries, edits live in under 60 s |
| D Sections | T-033 to T-048 | Whole page readable from CMS data in list layouts (also the reduced-motion site) |
| E 3D and motion | T-049 to T-075 | Scene, camera path, loader, cursor, four scroll patterns, adaptive quality |
| F Integrations | T-076 to T-081 | Visit counter, stats, analytics, working contact form |
| G Quality | T-082 to T-091 | SEO, 404 page, audits passed |
| H Launch | T-092 to T-095 | Domain live, Search Console, runbook, acceptance checklist |
| Added after planning | T-096 | Approved commit titles and Writing final-card wording, ahead of the import |

Skills by phase: `scroll-world-storytelling`, `threejs`, `cinematic-scroll-storytelling` (A, E); `editorial-portfolio-chapters` (D); `scroll-progress-timeline` (T-069 to T-072); `pointer-trail-emitter` (T-007, T-066); `ambient-section-particles` (T-059); `optimize-web-animations` (every E task, T-075); `audit-reference-originality` (T-002, T-091).

## Questions

Questions 1 to 12 were answered by the owner on 2026-11-16. Each keeps its number and the task it blocked. Question 13 came out of answer 2 and is open. The "Effect" line names the tasks that changed because of the answer.

### Answered

1. **Footer visits number. Answered.** The spec says "unique daily visitors (once per visitor per day, bots skipped)"; `content.md` says "total site visits". Should the footer show a running total where each visitor adds at most one a day, today's unique visitors, or both, and under what label?
   - Answer: a running total where each visitor adds at most one a day, bots skipped, labelled "visits". This is the design already in decision 0018.
   - Effect: T-001, T-048, T-076, T-077, T-078. Was blocking T-077; now clear.
2. **Hashnode. Answered.** What is the publication URL? Are there at least four posts today? May post cards also point to LinkedIn write-ups, given the last card says "Read everything on Hashnode"?
   - Answer: 1 to 3 posts today, so Writing shows the cards that exist plus the final card, and one, two or three posts must all render cleanly. Post cards may link to Hashnode or to LinkedIn write-ups, so each post has a source (Hashnode or LinkedIn), shown as a small label on its card, and the final card's wording covers both. The Hashnode publication URL is still `[FILL]`; the owner adds it in Studio.
   - Effect: T-001 (spec wording, and decision 0021, which supersedes 0001 for the post model), T-023, T-025, T-043, T-073, T-094, T-096. Raised question 13. Was blocking T-043; now clear.
3. **Commit-style titles** for the five roles are not in `content.md`. Will the owner write them, or should drafts be prepared for approval? **Answered.**
   - Answer: draft them from the resume bullets in `content.md` and show them to the owner for approval before they go into the import.
   - Effect: new T-096 (drafting and approval), T-030, T-031, T-039. Was blocking T-039; the approved titles must be in Sanity before T-039 is checked.
4. **The two `[CHECK]` items.** May the EY work name the Microsoft engagement and KubeMentor? **Answered.**
   - Answer: leave both out for now. The importer keeps holding them back, and EY shows one generic highlight ("Automate cloud delivery with Azure, GitHub Actions and Terraform") until the owner has confirmed with their manager.
   - Effect: T-030, T-031, T-039, T-090, T-094, T-096 (EY's commit title must not use the held-back items). Was blocking T-031; now clear.
5. **Section headings.** `content.md` gives headings only for Hero and Contact. May the others be seeded from the spec's section names? **Answered.**
   - Answer: yes, seed them from the spec's section names (Technical skills, About, Experience, Projects, Writing, Certifications & training, Where I'm heading). The owner can edit them in Studio. Hero and Contact keep the headings in `content.md`.
   - Effect: T-030, T-031, T-033. Was blocking T-031; now clear.
6. **The 15 `[FILL]` values:** Hashnode URL and host; Marslab stack; Linux Foundation language; repo links for four projects and a demo link for Discord Clone; three project covers; the AZ-900 date; two credential links. **Answered; the values are still to come.**
   - Answer: the owner will gather them over the coming days. T-090 and T-095 keep blocking launch on them.
   - Count: 15 are listed above. Answer 12 fills one (the "This portfolio" repo link), leaving 14. The Hashnode "publication host" repeats the publication URL now that no API is called, so T-001 proposes merging the two, which would leave 13.
   - Effect: T-090, T-095. Still needed before T-095.
7. **Domain and sender.** Is there a domain, and which? If not, does the site launch on the `vercel.app` address? Which email is the Resend account under? **Answered.**
   - Answer: no domain yet. The site launches first on its `*.vercel.app` address, and the owner buys the domain through Vercel at T-092. The Resend account is under subhranilrahaofficial@gmail.com.
   - Effect: T-018, T-080, T-092. Was blocking T-080 and T-092; T-080 goes ahead without a domain, and its plan confirms what Resend allows until T-092.
8. **Test phone.** Which phone or phones will be used for testing? That defines "mid-range" for the 30 fps fallback and the LCP target. **Answered.**
   - Answer: an iPhone (iOS Safari) only; there is no Android device. iPhone pinning, address-bar resize and the 30 fps fallback are the main phone checks, and the "mid-range phone" LCP and frame-rate targets are measured on the iPhone. Android is covered by browser emulation only; in T-089 and the audits its rows read "emulation only, not tested on real hardware", never "pass".
   - Effect: "How every task runs", T-010, T-013, T-041, T-049, T-050, T-060, T-065, T-067, T-070, T-072, T-087, T-089, T-095. First needed at T-010, where the iPhone model and iOS version are recorded.
9. **Additions beyond the spec:** T-019 (tests and CI), the `/resume` redirect (T-034), `pnpm env:check` (T-016) and `pnpm content:check` (T-090). Keep or strike? **Answered.**
   - Answer: keep all four.
   - Effect: T-016, T-019, T-034, T-090. Decision 0007 stays Proposed until T-019 confirms it.
10. **Loader.** On every full page load, or once per browser session? **Answered.**
    - Answer: on every full page load. Keep the 3-second cap and the CSS failsafe. The frequency is one named setting in code, not a CMS field, so switching to once per session later is a one-line change. T-065 measures LCP on repeat loads as well as first loads. If the loader on every load makes the spec's LCP target (under 2.5 s) or Lighthouse mobile Performance (85) fail, the choice is not changed silently: the numbers are reported, a risk is recorded in `docs/architecture.md`, and the owner is asked whether to switch to once per session.
    - Effect: T-001 (spec wording), T-065. Was blocking T-065; now clear.
11. **Copyright line.** Fixed text from Sanity ("© 2026 Subhranil Raha"), or the current year computed with the name? **Answered.**
    - Answer: computed: the current year plus the owner's name, not stored in the CMS.
    - Effect: T-001 (`content.md` note), T-023, T-030, T-048. Was blocking T-048; now clear.
12. **Is the GitHub repo public?** It decides the "This portfolio" link. **Answered.**
    - Answer: yes, public from the start, so the "This portfolio" link can be filled in. The `origin` remote is `https://github.com/SubhranilRaha/SubhranilRahaPortfolio`; T-001 shows the exact edit to `content.md` for approval.
    - Effect: T-001, T-031. Was blocking T-031; now clear.

### Open

13. **Footer post count.** *(new, from answer 2)* The footer shows a post count, and posts can now come from Hashnode or LinkedIn. Should the count include all posts (label "posts"), or only Hashnode posts (the spec's "Hashnode post count")? Recommendation: all posts, so the number matches the cards in Writing. Blocks T-078, and settles one line of the footer-stats wording in T-001.

## In progress

## To do

### Before Phase A

- **T-001 Bring the spec, rules and content notes in line with decisions 0001 to 0003 and the recorded answers.** Amend the spec, CLAUDE.md, `content.md` and `docs/architecture.md`, and write decision 0021. The exact wording is shown for approval before the commit.
  - Files: `docs/specs/0001-portfolio.md`, `CLAUDE.md`, `content.md` (notes, plus the one link from answer 12), `docs/architecture.md`, `docs/decisions/0021-writing-posts-have-a-source.md`, `docs/decisions/0001-writing-source.md` (status line only)
  - Needs: nothing. Question 13 settles one line (the footer post count).
  - Done when:
    - Decisions 0001 to 0003: `grep -rn "GraphQL" CLAUDE.md docs/specs content.md` finds nothing; the image rule in CLAUDE.md names the scene-art exception; the spec describes the project detail view as an overlay; the phone notes in `content.md` match the spec; CLAUDE.md's opening lines point to `docs/architecture.md`.
    - Answers: the spec's footer stats read "visits" (a running total, each visitor at most once a day, bots skipped) plus the post count; the spec says posts carry a source (Hashnode or LinkedIn) and the final Writing card covers both; the spec says the loader shows on every full page load; `content.md` marks the copyright line as computed (not imported), has the "This portfolio" repo link filled in from the `origin` remote, marks the two EY `[CHECK]` highlights as held back by decision, and proposes merging the Hashnode "publication host" line into the publication URL.
    - Architecture and records: `docs/architecture.md` reflects the answers (post source, "visits" label, computed copyright, the loader setting, iPhone-only phone checks, launch on `vercel.app` before the domain, 96 tasks); decision 0021 records the post source field and the two-source final card and supersedes 0001; 0001's status line reads "Superseded by 0021".

### Phase A: design study

- **T-002 Kage reference registry.** Capture the reference once, as evidence for the launch audit and as a do-not-copy list for the studies.
  - Files: `docs/audits/kage-reference.md`, `.gitignore` (adds `docs/audits/captures/`)
  - Needs: T-001
  - Done when: the registry lists the URL, capture date, every captured file with its SHA-256, and any gaps; the do-not-copy list covers motifs, copy, palette, compositions and choreography; `git status` shows no captured file staged.
- **T-003 Story map and style bible.** Map the ten chapters onto the six stations and define three art directions on paper before any code.
  - Files: `docs/design/style-bible.md`
  - Needs: T-002
  - Done when: a beat ledger gives each chapter its station, one motion verb and a scroll weight; directions A, B and C each define palette values inside the CLAUDE.md palette rule, a display and a mono font with licences, material and light language, composition and three exclusions; every text and background pair lists a contrast ratio of at least 4.5:1; the owner approves or edits the directions.
- **T-004 Study kit.** Set up `studies/` so each study is one HTML file that runs with no build step and no network.
  - Files: `studies/README.md`, `studies/index.html`, `studies/vendor/three/` (pinned build and licence), `studies/vendor/fonts/` (open-licence WOFF2 files and licences)
  - Needs: T-003
  - Done when: `python3 -m http.server 4173 -d studies` serves a launcher listing the variants; the Network tab shows no request to another host; the console prints the three.js revision the app will pin.
- **T-005 Variant A, part 1: shell and hero shot.**
  - Files: `studies/variant-a.html`
  - Needs: T-004
  - Done when: chapters 00 to 02 show their real copy from `content.md` as HTML text over a fixed canvas; the terminal station renders in direction A; resizing keeps the picture undistorted; pixel ratio is capped at 2 (1.5 on touch); hiding the tab stops the frame counter.
- **T-006 Variant A, part 2: first camera move.** Second station, the scroll-driven move between the two, cutout placeholders, reduced-motion version.
  - Files: `studies/variant-a.html`
  - Needs: T-005
  - Done when: scrolling flies terminal to toolchain and scrolling back returns identical frames; two placeholder cutouts stay pinned with slight parallax and never cover text; with reduced motion on, a still and plain layout replace the canvas; the on-page counter reads 60 fps.
- **T-007 Variant A, part 3: loader, cursor trail, touch ripple.**
  - Files: `studies/variant-a.html`
  - Needs: T-006
  - Done when: the loader counts real load progress and lifts within 3 s; the mouse trail keeps even spacing at slow and fast speeds; a tap in touch emulation makes one ripple; none of the three runs under reduced motion.
- **T-008 Variant B.** A second direction with a different field colour, materials, light, type pairing and composition; same scope as A.
  - Files: `studies/variant-b.html`
  - Needs: T-007
  - Done when: B passes the checks of T-005 to T-007; the five-point difference checklist in `studies/README.md` is ticked with a screenshot pair; the diff against A is reported.
- **T-009 Variant C.** A third direction under the same rules.
  - Files: `studies/variant-c.html`
  - Needs: T-007
  - Done when: as T-008, and C also differs from B on all five points.
- **T-010 Choose the direction.**
  - Files: `docs/decisions/0004-visual-direction.md`, `docs/design/style-bible.md` (reduced to the chosen direction, final tokens)
  - Needs: T-008, T-009. You: view all three on desktop and on the iPhone (note its model and iOS version, which later fps and LCP numbers refer to), then pick one or a mix.
  - Confirms: decision 0004 (completes it with the chosen direction)
  - Done when: decision 0004 is Accepted and names the variant; the style bible holds one final table of colour, type, spacing and motion tokens.
- **T-011 Asset brief.** The list of images for the owner to generate.
  - Files: `docs/design/asset-brief.md`
  - Needs: T-010
  - Done when: a table lists every foreground cutout and still with id, chapter, subject, orientation, pixel size, transparency, safe area and file name; one shared style paragraph is given to paste unchanged into every prompt; a do-not list is included (no logos or brand marks, no text, nothing on the Kage do-not-copy list); the drop folder and naming rule are stated; the owner confirms the images can be generated from it.
- **T-012 Master study, part 1.** Extend the chosen variant with stations 3 and 4 (pipeline, cloud network) and path timing for all chapters.
  - Files: `studies/master.html`
  - Needs: T-010
  - Done when: the camera visits four stations in chapter order and holds where Experience and Projects will pin; reverse scroll restores each state.
- **T-013 Master study, part 2.** Stations 5 and 6 (cluster, GPU racks), the end of the path, and the performance budget.
  - Files: `studies/master.html`, `docs/design/style-bible.md` (camera keyframe table, budget)
  - Needs: T-012. You: iPhone check.
  - Done when: the full path runs from hero to footer; draw calls, triangles and frame time are recorded for desktop and for the mobile setting (pixel ratio 1.5, 40 % particles); 60 fps on the Mac and at least 30 fps on the iPhone; cutout slots use the ids from the asset brief.

### Phase B: scaffold

- **T-014 Next.js skeleton.** Next 16 App Router, TypeScript strict and Tailwind 4 on pnpm, versions pinned. Generated with the official tool in a scratch folder, then copied in, because the repo is not empty.
  - Files: `package.json`, `pnpm-lock.yaml`, `.nvmrc`, `tsconfig.json`, `next.config.ts`, `postcss.config.mjs`, `src/app/layout.tsx`, `src/app/(site)/layout.tsx`, `src/app/(site)/page.tsx`, `src/app/globals.css`
  - Needs: T-010. You: approve installing pnpm.
  - Confirms: decision 0005
  - Done when: `pnpm dev` serves a blank page at `localhost:3000`; `pnpm build` passes; `tsconfig.json` has `"strict": true`; `pnpm ls next react typescript` shows the versions pinned in decision 0005.
- **T-015 Lint, format, typecheck.**
  - Files: `eslint.config.mjs`, `.prettierrc.json`, `.prettierignore`, `package.json`
  - Needs: T-014
  - Done when: `pnpm lint`, `pnpm typecheck` and `pnpm format:check` exit 0; adding `const x: any = 1` makes `pnpm lint` fail (then removed).
- **T-016 Typed env module.** One module that validates variables and fails fast. Variables are added to it task by task as integrations arrive, and its names are reconciled with the existing `.env.example`. The `pnpm env:check` script is an approved addition (answer 9).
  - Files: `src/env.ts`, `scripts/check-env.ts`, `.env.example`, `.claude/settings.json`, `package.json`
  - Needs: T-014. You: apply or confirm the deny-rule change (replace `Read(./.env.*)` with `Read(./.env.local)`, `Read(./.env.*.local)`, `Read(./.env.development)`, `Read(./.env.production)`, `Read(./.env.test)`; keep `Read(./.env)`).
  - Done when: `pnpm build` without `NEXT_PUBLIC_SITE_URL` fails and names the variable, and passes with it; `pnpm env:check` confirms every variable in `src/env.ts` is documented in `.env.example`; `.env.example` can be read while a read of `.env.local` is still refused.
- **T-017 Tokens and fonts.**
  - Files: `src/app/globals.css`, `src/app/fonts.ts`, `src/app/fonts/`, `src/app/layout.tsx`
  - Needs: T-010, T-015
  - Confirms: decision 0006
  - Done when: a temporary swatch page matches the style bible's colours and type scale; fonts are served from the site's own origin; Lighthouse reports layout shift 0 on that page; Tab shows a visible focus ring.
- **T-018 First deploy.**
  - Files: none expected
  - Needs: T-016. You: import the GitHub repo in Vercel, add the env variable (`NEXT_PUBLIC_SITE_URL` is the production `*.vercel.app` address until T-092 changes it), approve `git push`.
  - Done when: the `*.vercel.app` URL shows the blank page; the build log shows pnpm and the pinned Node version; a later push deploys by itself.
- **T-019 Tests and CI (approved addition, answer 9).** Vitest for pure logic and one GitHub Actions workflow.
  - Files: `vitest.config.ts`, `src/lib/smoke.test.ts`, `.github/workflows/ci.yml`, `package.json`
  - Needs: T-015
  - Confirms: decision 0007
  - Done when: `pnpm test` passes; the GitHub Actions run for the commit shows lint, typecheck, test and build green.

### Phase C: CMS

- **T-020 Sanity wiring and Studio at `/studio`.**
  - Files: `sanity.config.ts`, `sanity.cli.ts`, `src/app/studio/[[...tool]]/page.tsx`, `src/app/studio/layout.tsx`, `src/sanity/client.ts`, `src/env.ts`, `.env.example`
  - Needs: T-018. You: create the free Sanity project and `production` dataset, add the local and Vercel URLs as CORS origins, add the project id to `.env.local` and Vercel.
  - Confirms: decision 0008
  - Done when: `/studio` loads locally and on Vercel and the owner can sign in; it shows none of the site chrome; its HTML carries `noindex`.
- **T-021 Shared field types.** Image with required alt text and hotspot, rich text, SEO, chapter copy.
  - Files: `src/sanity/schemaTypes/objects/imageWithAlt.ts`, `richText.ts`, `seo.ts`, `chapterCopy.ts`, `src/sanity/schemaTypes/index.ts`
  - Needs: T-020
  - Done when: in a scratch document an image without alt text cannot be published; the hotspot and crop tool opens; the caption field is optional.
- **T-022 Site settings.**
  - Files: `src/sanity/schemaTypes/documents/siteSettings.ts`
  - Needs: T-021
  - Done when: fields exist for name, title line, location, public email, GitHub, LinkedIn and Hashnode links, resume and SEO; uploading a non-PDF as the resume is rejected.
- **T-023 Home page copy.** One document holding the copy of every chapter.
  - Files: `src/sanity/schemaTypes/documents/homePage.ts`
  - Needs: T-021
  - Confirms: decision 0009
  - Done when: Studio shows one tab per chapter (loader, hero, skills, about, experience, projects, writing, certifications, heading, contact, footer, 404) with its label, heading, intro and optional caption; About has rich text and a quick-facts list; the Writing tab also holds the wording of the final card (answer 2); there is no copyright field, because the footer computes it (answer 11).
- **T-024 Skills, experience and roadmap types.**
  - Files: `src/sanity/schemaTypes/documents/skillGroup.ts`, `experience.ts`, `milestone.ts`
  - Needs: T-021
  - Done when: one of each can be created; experience requires role, company, type and start date; ticking "current" hides the end date; type and status are fixed option lists.
- **T-025 Project, certification and post types.**
  - Files: `src/sanity/schemaTypes/documents/project.ts`, `certification.ts`, `post.ts`
  - Needs: T-021
  - Done when: a project cover needs alt text; a seventh gallery image is refused; a certification with no images saves; a post needs title, link, date and a source (Hashnode or LinkedIn), while reading time, tags and cover are optional (a LinkedIn write-up may have none of them).
- **T-026 Studio structure.**
  - Files: `src/sanity/structure.ts`, `sanity.config.ts`
  - Needs: T-022 to T-025
  - Done when: the sidebar reads Site settings, Home page copy, Skills, Experience, Projects, Writing, Certifications, Roadmap; the two single documents cannot be duplicated or deleted; reordering skills, projects and milestones persists.
- **T-027 Typed fetch layer.**
  - Files: `src/sanity/fetch.ts`, `src/sanity/queries.ts`, `sanity.types.ts`, `package.json`
  - Needs: T-026
  - Confirms: decision 0010
  - Done when: `pnpm typegen` regenerates the types; misspelling a field inside a query makes `pnpm typecheck` fail; the home page prints the site name from Sanity; the build output marks `/` as static.
- **T-028 Section queries.**
  - Files: `src/sanity/queries.ts`, `sanity.types.ts`
  - Needs: T-027
  - Done when: one typed query per section returns the expected shape in Studio's Vision tool; no generated result type contains `any`; a grep finds no GROQ outside `queries.ts`.
- **T-029 Sanity image component.**
  - Files: `src/sanity/image.ts`, `src/components/ui/SanityImage.tsx`
  - Needs: T-028
  - Confirms: decision 0011
  - Done when: a test image renders a `srcset` on `cdn.sanity.io` with `auto=format`; a blur placeholder shows on a throttled connection; moving the hotspot in Studio changes the crop; no `/_next/image` request is made; omitting `alt` is a type error.
- **T-030 `content.md` parser (dry run).**
  - Files: `scripts/import-content/parse.ts`, `types.ts`, `index.ts`, `parse.test.ts`, `package.json`
  - Needs: T-025, T-096
  - Done when: `pnpm import:content --dry-run` reports 5 skill groups, 5 roles (each with its approved commit title), 4 projects, 4 certifications, 4 milestones, 12 captions, 5 quick facts and 7 section headings (the section titles in `content.md`, which match the spec's names), and lists every `[FILL]` and `[CHECK]` marker with its line number; it skips the footer copyright line (answer 11); it makes no network request.
- **T-031 Import writer.**
  - Files: `scripts/import-content/write.ts`, `index.ts`, `.env.example`
  - Needs: T-030, T-027, T-096. You: create a write token and add it to `.env.local` only, never to Vercel.
  - Done when: the first run creates the documents and a second run reports 0 changes; Studio content matches `content.md`; list items marked `[CHECK]` are held back and named in the report, so EY has exactly one highlight in Studio (answer 4); the 7 section headings, 5 commit titles, final-card wording and the "This portfolio" repo link are present; `[FILL]` fields are empty rather than holding placeholder text.
- **T-032 Revalidation webhook.**
  - Files: `src/app/api/revalidate/route.ts`, `src/env.ts`, `.env.example`
  - Needs: T-028, T-018. You: create the webhook in Sanity with the shared secret.
  - Done when: publishing a change to the name in Studio shows on the deployed site in under 60 s with no redeploy (timed); a request with a wrong signature gets 401; Sanity's webhook log shows 200.

### Phase D: sections

Each section is built here in its list layout, which is also what reduced-motion visitors and visitors without JavaScript get. Phase E adds the scroll pattern on top. The spec fixes a pattern for four sections only; for Skills, About, Where I'm heading and Contact a layout is proposed in the task's own plan.

- **T-033 Page shell and chapter parts.**
  - Files: `src/app/(site)/page.tsx`, `src/components/chrome/ChapterSection.tsx`, `ChapterLabel.tsx`, `SectionHeading.tsx`, `Caption.tsx`, `src/lib/chapters.ts`
  - Needs: T-028, T-017, T-031
  - Confirms: decision 0012
  - Done when: nine chapters appear in spec order with label, heading and caption from Sanity (headings as seeded from the spec's section names, answer 5); deleting a caption in Studio removes it from the page; the outline is one h1 followed by h2s; `/#projects` lands on Projects.
- **T-034 Nav bar and resume link.** The `/resume` redirect is an approved addition (answer 9).
  - Files: `src/components/chrome/Nav.tsx`, `NavLink.tsx`, `ResumeButton.tsx`, `SkipLink.tsx`, `src/app/resume/route.ts`, `src/app/(site)/layout.tsx`
  - Needs: T-033, T-032
  - Done when: the sticky nav scrolls to each section and marks the current one; `/resume` downloads the PDF from Sanity, and a newly uploaded PDF is served within 60 s; with no PDF uploaded the button is hidden.
- **T-035 Mobile menu.**
  - Files: `src/components/chrome/MobileMenu.tsx`, `MenuButton.tsx`
  - Needs: T-034
  - Done when: at 375 px the hamburger opens a menu that traps focus, closes on Esc and returns focus; the Resume button stays visible in the bar; every target is at least 44 px.
- **T-036 Hero.**
  - Files: `src/components/sections/Hero.tsx`
  - Needs: T-033
  - Done when: heading, intro, both buttons, scroll cue and caption match Sanity; "View my work" scrolls to Projects; DevTools names the h1 as the largest contentful paint.
- **T-037 Skills.**
  - Files: `src/components/sections/Skills.tsx`, `SkillGroup.tsx`
  - Needs: T-033
  - Done when: five groups render from Sanity; a skill added in Studio appears within 60 s; no horizontal scroll at 375 px.
- **T-038 About.**
  - Files: `src/components/sections/About.tsx`, `src/components/ui/RichText.tsx`, `QuickFacts.tsx`
  - Needs: T-033
  - Done when: three paragraphs and five quick facts render from Sanity as selectable text; a link added in Studio renders as a link.
- **T-039 Experience, list layout.**
  - Files: `src/components/sections/Experience.tsx`, `ExperienceItem.tsx`, `src/lib/experience.ts`
  - Needs: T-033
  - Done when: roles appear newest first in an ordered list with dates, type, highlights, stack, short hash and commit title; EY is on `main` and the others on branches; EY renders cleanly with its single highlight and a role with an empty stack renders cleanly (answers 4 and 6); the section reads correctly with JavaScript disabled.
- **T-040 Projects, grid layout.**
  - Files: `src/components/sections/Projects.tsx`, `ProjectCard.tsx`
  - Needs: T-033, T-029
  - Done when: cards show cover, title, summary and tech from Sanity; a project with no cover still renders a tidy card; one column at 375 px, two or more at 1440 px.
- **T-041 Lightbox.**
  - Files: `src/components/ui/Lightbox.tsx`, `src/lib/useSwipe.ts`
  - Needs: T-029
  - Done when: arrow keys and Esc work; focus stays inside and returns to the trigger; a swipe changes image on the iPhone; each image carries its alt text.
- **T-042 Project detail dialog.**
  - Files: `src/components/sections/ProjectDialog.tsx`, `ProjectGallery.tsx`, `ProjectCard.tsx`
  - Needs: T-040, T-041
  - Done when: click or Enter on a card opens a dialog with summary, tech, links and gallery; `/#project-<slug>` opens it directly; Esc and the browser Back button close it; the page behind does not scroll.
- **T-043 Writing, list layout.**
  - Files: `src/components/sections/Writing.tsx`, `PostCard.tsx`
  - Needs: T-033, T-029
  - Done when: up to four posts show title, date and a small source label ("Hashnode" or "LinkedIn") and, when present, cover, reading time and tags, and open in a new tab; the final card shows its wording from Sanity and one link per source whose URL exists in site settings (so only LinkedIn until the Hashnode URL is filled in); one, two and three posts each render cleanly (checked with all three); no posts shows only the final card. Which LinkedIn address the card uses (the profile link from site settings, unless the owner wants a separate one) is settled in this task's plan.
- **T-044 Certifications panel.**
  - Files: `src/components/sections/Certifications.tsx`, `CheckRow.tsx`, `StatusIcon.tsx`, `src/lib/certifications.ts`
  - Needs: T-033, T-029
  - Done when: one row per entry shows badge, status icon, name, issuer and date; the summary line "N checks · X passed · Y running" changes when a status changes in Studio; rows without a badge stay aligned; the spinner is still under reduced motion.
- **T-045 Certification row details.**
  - Files: `src/components/sections/CheckRow.tsx`, `CheckDetails.tsx`
  - Needs: T-044, T-041
  - Done when: a row expands from the keyboard and announces its state; it shows the certificate image (opening the lightbox) and "Verify credential" when present; rows with neither offer no expansion.
- **T-046 Where I'm heading.**
  - Files: `src/components/sections/Roadmap.tsx`, `MilestoneRow.tsx`
  - Needs: T-033
  - Done when: the intro and four milestones (stage, focus, status) render in order from Sanity; the layout reuses none of the four reserved patterns.
- **T-047 Contact form (interface only).**
  - Files: `src/components/sections/Contact.tsx`, `ContactForm.tsx`, `src/lib/contact.ts`
  - Needs: T-033
  - Done when: name, email and message have labels and inline errors that screen readers announce; the hidden honeypot is skipped by Tab; submitting shows the designed failure state with a working mailto link (the endpoint arrives in T-080).
- **T-048 Footer.**
  - Files: `src/components/chrome/Footer.tsx`, `FooterStats.tsx`
  - Needs: T-033
  - Done when: line, links and caption come from Sanity; a link whose URL is empty (the Hashnode link, until the owner fills it in) is not rendered; the copyright reads "© <current year> <name from site settings>", computed when the page renders and not stored in Sanity (answer 11), so it rolls over at the first re-render after New Year; three stat slots, the first labelled "visits" (answer 1), show a dash at their final width, so nothing shifts when numbers arrive.

### Phase E: 3D and motion

- **T-049 Motion foundation.** GSAP ScrollTrigger and Lenis, plus the small store the scene reads scroll progress from.
  - Files: `src/components/motion/SmoothScroll.tsx`, `src/lib/motion.ts`, `src/lib/scrollStore.ts`, `src/app/(site)/layout.tsx`
  - Needs: T-048
  - Confirms: decision 0013
  - Done when: wheel scrolling is smoothed on desktop; under reduced motion no smooth-scroll instance exists; nav links and the dialog scroll lock still work; on the iPhone the address bar collapsing causes no jump.
- **T-050 Scene shell.** The lazy-loaded canvas behind the HTML and its static fallback.
  - Files: `src/components/scene/SceneRoot.tsx`, `SceneCanvas.tsx`, `StaticScene.tsx`, `SceneErrorBoundary.tsx`, `src/app/(site)/layout.tsx`
  - Needs: T-049, T-013
  - Confirms: decision 0014
  - Done when: a placeholder mesh renders behind the HTML; the three.js chunk is requested only after first paint; under reduced motion the static image shows and no WebGL context is created; hiding the tab stops rendering; Lighthouse mobile Performance is still at least 85 (baseline recorded, and also read on the iPhone; this task's plan says how LCP and frame rate are read on iOS Safari and what stands in if Safari cannot report LCP).
- **T-051 Scene base.** Colours, lights, fog and shared materials ported from the master study.
  - Files: `src/components/scene/tokens.ts`, `materials.ts`, `Environment.tsx`
  - Needs: T-050
  - Confirms: decision 0015
  - Done when: background, fog and light match a screenshot of the master study's hero shot placed side by side.
- **T-052 Camera path and scroll conductor.**
  - Files: `src/components/scene/cameraPath.ts`, `CameraRig.tsx`, `src/components/motion/ChapterTriggers.tsx`
  - Needs: T-051
  - Done when: with marker boxes at the six station positions, scrolling top to bottom visits them in chapter order and scrolling back restores the same frames; a fast flick never overshoots; a dev overlay shows the chapter number matching the section on screen at every boundary.
- **T-053 Station: terminal.**
  - Files: `src/components/scene/stations/Terminal.tsx` and its geometry factory
  - Needs: T-052
  - Done when: the station matches the master study at its camera shot; draw calls and triangles stay inside the T-013 budget on the dev overlay; ten visits to `/studio` and back leave GPU memory counts unchanged.
- **T-054 Station: toolchain.**
  - Files: `src/components/scene/stations/Toolchain.tsx` and its geometry factory
  - Needs: T-052
  - Done when: same three checks as T-053.
- **T-055 Station: pipeline.**
  - Files: `src/components/scene/stations/Pipeline.tsx` and its geometry factory
  - Needs: T-052
  - Done when: same three checks as T-053.
- **T-056 Station: cloud network.**
  - Files: `src/components/scene/stations/CloudNetwork.tsx` and its geometry factory
  - Needs: T-052
  - Done when: same three checks as T-053.
- **T-057 Station: cluster.**
  - Files: `src/components/scene/stations/Cluster.tsx` and its geometry factory
  - Needs: T-052
  - Done when: same three checks as T-053.
- **T-058 Station: GPU racks.**
  - Files: `src/components/scene/stations/GpuRacks.tsx` and its geometry factory
  - Needs: T-052
  - Done when: same three checks as T-053.
- **T-059 Scene particles.**
  - Files: `src/components/scene/Particles.tsx`
  - Needs: T-051
  - Done when: ambient motes match the study; the count follows the quality setting (100 % down to 40 %); still under reduced motion; memory stays flat over 30 s.
- **T-060 Adaptive quality.** Quality settings and the performance monitor that steps between them.
  - Files: `src/components/scene/quality.ts`, `QualityProvider.tsx`
  - Needs: T-058, T-059
  - Confirms: decision 0016
  - Done when: under 6x CPU throttling the quality steps down (logged) and finally swaps to the static image with no flash or scroll jump; touch devices start at pixel ratio 1.5 or less, 40 % particles and no shadows; the iPhone holds 30 fps or falls back (thresholds are tuned on the iPhone; Android is emulation only).
- **T-061 Finishing pass (only if decision 0004 calls for post-processing).**
  - Files: `src/components/scene/Effects.tsx`
  - Needs: T-060
  - Done when: the effect matches the study on desktop, is lighter on the mobile setting and off at the lowest; 60 fps on desktop holds.
- **T-062 Scene art pipeline.**
  - Files: `scripts/optimize-scene-art.ts`, `src/components/scene/art.ts`, `public/scene/`, `.gitignore`, `package.json`
  - Needs: T-014. You: the art generated from the T-011 brief.
  - Done when: `pnpm scene:art` converts the originals to WebP at the brief's sizes; each file is under the brief's size budget; the ids in `art.ts` equal the brief's ids; originals are git-ignored.
- **T-063 Foreground cutouts.**
  - Files: `src/components/scene/ForegroundCutouts.tsx`, `Cutout.tsx`
  - Needs: T-062, T-052
  - Done when: each chapter's cutouts stay pinned with slight parallax and never cover text at 375 or 1440 px; they are decorative (`alt=""`) and lazy below the fold; fixed in place under reduced motion.
- **T-064 Static scene image.**
  - Files: `src/components/scene/StaticScene.tsx`, `public/scene/`
  - Needs: T-062, T-050
  - Done when: reduced-motion and fallback visitors see the final still with a blur placeholder and correct crops at 375 and 1440 px; its file size is inside the brief's budget.
- **T-065 Loader.** Shows on every full page load (answer 10). The frequency is one named setting in code, not a CMS field.
  - Files: `src/components/chrome/Loader.tsx`, `src/lib/loadProgress.ts`, `src/lib/loaderConfig.ts`, `docs/architecture.md` (only if the LCP check below fails)
  - Needs: T-050, T-017
  - Confirms: decision 0017 (updated for answer 10)
  - Done when: the counter follows real loading (intermediate values on a throttled connection); content shows by 3 s at the latest, even with JavaScript blocked (the CSS failsafe, tested with scripts off); skipped under reduced motion; `LOADER_FREQUENCY` in `loaderConfig.ts` is the only place the frequency is set (`"every-load"` now; switching to `"once-per-session"` is a one-line change, shown by trying it); LCP is under 2.5 s and Lighthouse mobile Performance is at least 85 on a first load and on a repeat load with a warm cache (for example Lighthouse with storage reset disabled), with the loader on, and LCP is also read on the iPhone. If any of these fail, the setting is left unchanged: the numbers are reported, the risk is added to `docs/architecture.md`, the owner is asked whether to switch to once per session, and the task stays In progress until they answer.
- **T-066 Custom cursor.**
  - Files: `src/components/scene/CursorTrail.tsx`
  - Needs: T-050
  - Done when: the trail keeps even spacing at any hand speed; a resting pointer shows a faint breath, not a column; absent on touch devices; a designed still under reduced motion; links and form fields remain easy to target.
- **T-067 Touch ripple.**
  - Files: `src/components/scene/TouchRipple.tsx`
  - Needs: T-050. You: iPhone check.
  - Done when: a tap makes one ripple at the touch point; scrolling makes none; none with a mouse or under reduced motion.
- **T-068 Reveal motion for the unpatterned sections.**
  - Files: `src/components/motion/Reveal.tsx`, `SplitHeading.tsx`, the sections that use them
  - Needs: T-049
  - Done when: the hero heading and section headers reveal once on entry; all text is readable with JavaScript disabled; nothing moves under reduced motion; no layout shift.
- **T-069 Commit graph drawing.**
  - Files: `src/components/sections/experience/CommitGraph.tsx`, `src/lib/commitGraph.ts`, `commitGraph.test.ts`
  - Needs: T-039
  - Done when: an SVG draws `main` plus one merging branch per side role from Sanity data; adding a role in Studio adds a commit; the graph is hidden from screen readers, which get the list.
- **T-070 Commit graph scroll.**
  - Files: `src/components/sections/experience/CommitGraphScroll.tsx`, `Experience.tsx`
  - Needs: T-069, T-049. You: iPhone check.
  - Done when: the section pins; the marker moves commit to commit and the role panel changes in step, forward and backward; Tab reaches every role; the pin releases cleanly into Projects; the same works at 375 px and on the iPhone, including the address bar collapsing and expanding; reduced motion shows the list.
- **T-071 Deployment track.**
  - Files: `src/components/sections/projects/DeploymentTrack.tsx`, `Projects.tsx`
  - Needs: T-042, T-049
  - Done when: the section pins and vertical scrolling moves the cards sideways; tabbing to a card brings it into view; cards still open the dialog; reduced motion shows the grid.
- **T-072 Pipeline progress bar and iPhone tuning.**
  - Files: `src/components/sections/projects/PipelineProgress.tsx`, `DeploymentTrack.tsx`
  - Needs: T-071. You: iPhone check.
  - Done when: the bar and its stage markers agree with the active card at every boundary in both directions; on the iPhone the track follows vertical swipes smoothly, survives the address bar collapsing and never traps the scroll.
- **T-073 Stacked cards for Writing.**
  - Files: `src/components/sections/writing/CardStack.tsx`, `Writing.tsx`
  - Needs: T-043, T-049
  - Done when: each card pins while the next slides over it; the covered card scales down and dims; the final card ends the stack without overlapping Certifications; the stack works with 2, 3 and 4 cards (1 to 3 posts plus the final card), and with only the final card it is a plain card with no pin; reduced motion shows the list.
- **T-074 Checks-panel run sequence.**
  - Files: `src/components/sections/certifications/ChecksRun.tsx`, `Certifications.tsx`
  - Needs: T-045, T-049
  - Done when: on first entry the rows resolve to their status in order and the summary settles on the computed counts; in-progress rows keep a slow amber spinner; it does not replay; still under reduced motion.
- **T-075 Whole-page animation and leak pass.**
  - Files: fixes only, `docs/audits/animation-profile.md`
  - Needs: T-061 to T-074
  - Done when: profiles at top, middle and footer, and at 375 px, show nothing animating off screen or in a hidden tab; ten round trips to `/studio` leave canvas, listener and DOM-node counts unchanged; 60 fps on desktop throughout.

### Phase F: integrations

- **T-076 Visit counting logic.**
  - Files: `src/lib/visits.ts`, `src/lib/redis.ts`, `src/lib/visits.test.ts`, `src/env.ts`, `.env.example`
  - Needs: T-016. You: create the free Upstash database and add its URL and token.
  - Confirms: decision 0018
  - Done when: tests show the same visitor on the same day maps to one key, a new day to a new key, and known bot user agents are rejected; a test asserts no raw IP address is ever written; the stored total counts each visitor at most once a day (answer 1).
- **T-077 Visit endpoint and beacon.**
  - Files: `src/app/api/visit/route.ts`, `src/components/chrome/VisitBeacon.tsx`
  - Needs: T-076, T-048
  - Done when: a first browser visit raises the total by one; a reload the same day does not; `curl -A Googlebot` does not; localhost and preview deployments do not; with Redis unreachable the footer shows a dash and the page works.
- **T-078 Footer stats.**
  - Files: `src/lib/github.ts`, `src/components/chrome/FooterStats.tsx`, `src/sanity/queries.ts`
  - Needs: T-077
  - Done when: the footer shows visits, public GitHub repositories and posts (what the post count includes is question 13); the repository number equals the one on the GitHub profile; with GitHub unreachable it shows the last known number or a dash, never an error.
- **T-079 Vercel Web Analytics.**
  - Files: `src/app/(site)/layout.tsx`, `package.json`
  - Needs: T-018. You: switch on Web Analytics in Vercel.
  - Done when: a visit appears in the Vercel dashboard; `/studio` sends no events.
- **T-080 Contact endpoint.** Validation, honeypot, rate limit, send through Resend.
  - Files: `src/app/api/contact/route.ts`, `src/lib/contact.ts`, `src/lib/rateLimit.ts`, `src/lib/contact.test.ts`, `src/env.ts`, `.env.example`
  - Needs: T-076, T-047. You: a Resend API key (the account is under subhranilrahaofficial@gmail.com). There is no domain until T-092 (answer 7); this task's plan confirms what Resend allows from its shared test sender until then.
  - Confirms: decision 0019
  - Done when, by `curl`: a valid message returns 200 and reaches the inbox within a minute with reply-to set to the sender; a bad email returns 400 with field errors; a filled honeypot returns 200 and sends nothing; the fourth request inside the window returns 429; the from address is a single environment value, so T-092 switches it to the domain without a code change.
- **T-081 Connect the form.**
  - Files: `src/components/sections/ContactForm.tsx`
  - Needs: T-080
  - Done when: the real form goes from sending to success and clears; server field errors appear on the right field; a 429 shows a wait message; a failure shows the mailto link; focus moves to the status message.

### Phase G: quality

- **T-082 Metadata.**
  - Files: `src/app/(site)/layout.tsx`, `src/app/studio/layout.tsx`
  - Needs: T-028
  - Done when: title, description, keywords, canonical, Open Graph and Twitter tags in the page source equal the SEO fields in Sanity; changing the description in Studio changes the source within 60 s.
- **T-083 Open Graph image.**
  - Files: `src/app/opengraph-image.tsx`, `src/app/fonts/` (a copy of the display font in a format the generator accepts)
  - Needs: T-082
  - Confirms: decision 0020
  - Done when: `/opengraph-image` returns a 1200 x 630 image with the name and title line from Sanity in the site's display font.
- **T-084 Sitemap, robots and Person JSON-LD.**
  - Files: `src/app/sitemap.ts`, `src/app/robots.ts`, `src/components/chrome/PersonJsonLd.tsx`
  - Needs: T-082
  - Done when: `/sitemap.xml` lists the home page with the production URL; `/robots.txt` disallows `/studio` and `/api` and names the sitemap; a schema validator reports a valid Person with no errors.
- **T-085 404 page.**
  - Files: `src/app/not-found.tsx`
  - Needs: T-033, T-064
  - Done when: an unknown URL returns status 404 with the caption from Sanity, a link home and the static scene image; no WebGL loads on it.
- **T-086 Accessibility audit.**
  - Files: fixes, `docs/audits/accessibility.md`
  - Needs: T-075, T-081
  - Done when: axe reports no serious or critical issue on home and 404; Lighthouse Accessibility is at least 95; a keyboard-only pass reaches nav, menu, every control, dialog and lightbox with visible focus; the page passes with reduced motion and at 200 % zoom.
- **T-087 Performance audit.**
  - Files: fixes, `docs/audits/performance.md`
  - Needs: T-075
  - Done when: three Lighthouse mobile runs on the production URL each give Performance at least 85, Best Practices at least 95 and SEO 100; LCP is under 2.5 s on the iPhone (model and iOS version recorded) and in Lighthouse's mobile run (an emulation, marked as such); the initial JavaScript contains no three.js; the console is clean.
- **T-088 Hygiene checks.**
  - Files: `next.config.ts` (security headers), `docs/audits/hygiene.md`
  - Needs: T-081
  - Done when: `pnpm env:check` passes; a scan of the repo and its history finds no secret; the rendered HTML contains no phone number; `pnpm audit` shows no high or critical issue, or each is listed with a reason.
- **T-089 Device and browser matrix.**
  - Files: `docs/audits/qa-matrix.md`
  - Needs: T-075. You: the iPhone rows.
  - Done when: the table is filled for Chrome, Safari and Firefox on desktop, for iOS Safari on the iPhone and for Android Chrome, at 375, 768, 1024 and 1440 px, per section and pattern; the iPhone rows cover rotation and address-bar resize, and widths the iPhone cannot show are marked as a resized desktop browser; every Android row reads "emulation only, not tested on real hardware", never "pass"; each failure is filed as a new task.
- **T-090 Content completeness gate (approved addition, answer 9).** Blocks launch until the `[FILL]` values are in (answer 6).
  - Files: `scripts/check-content.ts`, `package.json`
  - Needs: T-031
  - Done when: `pnpm content:check` lists every empty launch-required field, every unpublished draft and any leftover `[FILL]` text, and exits 0 only when none remain; the script's list of launch-required fields covers every `[FILL]` value in `content.md` (the values listed in answer 6); the two held-back EY highlights are listed as "held back by decision (answer 4)" and do not fail the check.
- **T-091 Originality audit against Kage.**
  - Files: `docs/audits/originality-kage.md`
  - Needs: T-002, T-075
  - Done when: the report follows the skill's format, covers all eight categories, cites evidence on both sides for every flag, attaches the inventory helper's output, and ends in "Clear in checked scope" or "Clear with low-risk similarities"; anything worse becomes tasks that block launch.

### Phase H: launch

- **T-092 Production domain.** Until now the site runs on its `*.vercel.app` address (answer 7). The owner buys the domain through Vercel here.
  - Files: `.env.example` (notes)
  - Needs: T-086 to T-091 (the audits ran on the `*.vercel.app` address). You: buy the domain through Vercel (a paid purchase), set `NEXT_PUBLIC_SITE_URL` to it, add the new origin and webhook URL in Sanity, verify the sending domain in Resend.
  - Done when: the domain serves the site over HTTPS and the other host form redirects; a Studio edit still shows within 60 s; a contact message arrives from the domain's sender; sitemap, canonical and share URLs use the domain; the sitemap, robots and Person JSON-LD checks from T-084 and one Lighthouse mobile run are repeated on the domain; what happens to the `*.vercel.app` address (redirect or canonical only) is decided in this task's plan.
- **T-093 Search Console.**
  - Files: `src/app/(site)/layout.tsx`, `src/env.ts` (only if the meta-tag method is used)
  - Needs: T-092. You: verify the property and submit the sitemap.
  - Done when: Search Console shows the property verified and the sitemap status as Success.
- **T-094 Editing runbook.**
  - Files: `docs/runbooks/editing-content.md`
  - Needs: T-092
  - Done when: using only the runbook the owner changes a caption, replaces the resume, adds a project with images, adds a certification and adds a post (choosing Hashnode or LinkedIn as its source), and each is live within 60 s; it also covers image sizes and alt text, replacing scene art, rotating secrets, adding the two held-back EY highlights once the manager confirms (answer 4), and what to do when an edit does not show.
- **T-095 Launch checklist.**
  - Files: `docs/audits/launch-checklist.md`, `docs/progress.md`
  - Needs: T-090, T-093, T-094
  - Done when: every acceptance criterion in the spec has a dated pass with evidence, with phone evidence taken from the iPhone and Android stated as emulation only (answer 8); `pnpm content:check` exits 0, so every `[FILL]` value is filled in and published (answer 6); tag `v1.0.0` exists.

### Added after planning

- **T-096 Draft commit titles and the Writing final-card wording for approval.** The five commit-style titles and the wording of the Writing final card (covering Hashnode and LinkedIn) are not in `content.md`. They are drafted, shown to the owner, and only then added to `content.md` and imported (answers 2 and 3).
  - Files: `content.md` (a "Commit title" line under each role, and the final-card wording under Writing; added only after approval)
  - Needs: T-001
  - Done when: drafts of all five commit titles and the final-card wording are shown to the owner; each is approved or edited by them; the approved text is in `content.md`; each title is a plain commit-style summary of that role's listed highlights and adds no claim they do not make; EY's title is based only on its one remaining highlight and does not mention the Microsoft engagement or KubeMentor (answer 4); none of the texts contains humour (CLAUDE.md keeps humour to one caption per section); the final-card wording covers both Hashnode and LinkedIn.

## Done
