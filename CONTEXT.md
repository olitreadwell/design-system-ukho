# UKHomeOffice/design-system context
> refreshed 2026-10-12 | upstream default: master @ 358c818abacc67643278ceadbfed64281d795b19 (2026-10-01 "Merge pull request #756 from UKHomeOffice/sshukor-patch-9")

## Identity & policies
- upstream: UKHomeOffice/design-system (Home Office Design System; TypeScript monorepo, pnpm workspaces; docs site design.homeoffice.gov.uk). English-first: yes (UK English; CI pins LANG/LC_ALL=en_GB.UTF-8).
- fork: olitreadwell/design-system-ukho (GitHub renamed it on fork because design-system/design-system-1/-2 were taken). Fork default branch: master.
- CLA/DCO: none found (no CONTRIBUTING at repo or org level; UKHomeOffice/.github has no CONTRIBUTING or PR template).
- AI-assisted PR policy: unstated (no AI policy file). Note the repo has merged a Copilot-autofix co-authored commit (42d2a338, 2026-09-25), so AI-assisted changes are not banned in practice.
- signed commits required: no (branch protection API 404; merges land from the web UI; no verify-commit-signatures workflow).
- PR template: none (checked repo root, .github/, docs/, and the org default). Use the pipeline 3-section fallback body.
- external tracker: none; issues + discussions stay on GitHub.

## Conventions (verified from merged PRs)
- branch naming: mixed, no dominant pattern. Merged heads seen: `sshukor-patch-9`, `feat/playwrightVisualChecks`, `feat/updateNode`, `feat/copilotInstructions`, `broken-link-fixes`, `accessibility-fixes`, `bobby-king`. `feat/<camelCase>` for features; plain kebab (`broken-link-fixes`) for docs/link sweeps.
- commit style: plain imperative sentences ("Correct link to plopfile.mjs in README") mixed with Conventional Commits ("chore: ...", "feat: ...").
- test command: `npm test` at the root (jest, 22 suites, 190 pass / 8 skip as of 2026-10-12 on fork master).
- build command: `cd apps/<app> && npm run build` (apps: docs, next-example, remix-example); libraries: `npm run libs:build`.
- required toolchain: Node 24 (.nvmrc `24`, package.json engines node >=22), pnpm 12.3.4 (`cp pnpm-lock-committed.yaml pnpm-lock.yaml` first). CI change-assurance.yml gates on node 22 + 24.
- CI checks that gate merge: Change assurance (Static analysis/CodeQL, Dependencies + Unit tests, Build libraries, Build application, Test application), Visual regression tests, plus a push-triggered Deploy that needs Netlify/Chromatic secrets (always red on a fork — fork artifact).
- how outside PRs actually get merged: slowly and irregularly. Merges in the last 12 months are dominated by two in-house accounts (sshukor, aaronrussellHO); the most recent clearly outsourced merges are #742 guermanc (2026-06-30) and #730 willrichards (2026-03-18). Review latency is days-to-weeks, not hours.

## Maintainer picture
- active committers: sshukor, aaronrussellHO; contributors LaurenShiel, willrichards, elliot-butler (docs/content).
- open PR backlog: ~19 open PRs (2026-10-12), several long-lived in-flight branches. Avoid files those branches touch.
- in-flight work to avoid (verified 2026-10-12): #754 feat/pnpmToNpm rewrites README.md + the whole toolchain (pnpm -> npm); #753 feat/trustedPublishing rewrites publish workflow + component package.json files; #749 contributing.md-fixing-links rewrites all three links in CONTRIBUTING.md; #717 edits content-style-guide.tsx; #747/#707 edit Header.tsx; #714 edits Footer.tsx; #745/#700 edit approved-tools.md.

## Issue-area health
- open issues: 59 (includes PRs). Mostly content/guidance requests rather than code bugs; there is no good-first-issue label in use.
- Areas with contested/redesign signals: none strongly flagged; the docs site is being steadily edited, so small content fixes are the low-risk entry point.
- Not attempted: no open+accepted+unassigned issue has been picked from this repo yet.

## Gap ledger (dedupe — READ FIRST, never re-pick)
- 2026-08-05 docs-dead-link (self-found) — pr-opened -> closed: fork PRs #1/#2 fixed the README reference links `pnpm-workspaces.yaml` and `plopfile.js` (renamed to `pnpm-workspace.yaml` / `plopfile.mjs`). Never merged upstream; both closed by us for branch renaming. Do NOT re-open: upstream later fixed the inline `plopfile.mjs` link (42d2a338), and the remaining two stale reference targets in README.md are still there but belong to that same closed pick (and README is being rewritten by #754 anyway).
- 2026-09-25, 2026-09-26 engine-failure — error: engine/run.sh exited 1 with no agent trace; nothing was produced or logged by the agent.
- 2026-10-12 docs-typos (self-found) — pr-opened: fork PR #8, 10 files, +18/-18, pure spelling fixes (see "Outcome log" below). Deliberately did NOT touch README.md (in flight in #754) or CONTRIBUTING.md (all three links already fixed in flight by #749).
- Lesson: this repo has no PR template and no CLA/signing gates, so the only guardrails are (a) avoid files with open in-flight PRs, and (b) keep doc sweeps small and text-only.

## Mined gaps (discovered, not yet attempted)
- 2026-10-12 `README.md:71` "mutliple" -> "multiple" and `README.md:88` "If you would like add more varieties" -> "like to add". Left alone because #754 rewrites README.md in flight; re-check after #754 lands. — status: proposed
- 2026-10-12 `README.md:92-94` all three reference links point at https://not-govuk.netlify.app/ which is dead (Netlify "site not found", 404). No verified replacement found yet (https://hods.netlify.app/ returns 200 but its ownership/relevance is unconfirmed). — status: proposed
- 2026-10-12 `README.md:90` + `CONTRIBUTING.md:7` link the community backlog at .../projects/1, which 404s (repo has no classic project #1; the Projects API returns 404). Covered by in-flight #749 for CONTRIBUTING.md; README copy still open. — status: proposed
- 2026-10-12 `components/ucdm-page/src/Page.tsx:39` JSDoc "diplayed" -> "displayed" and `components/status-message/README.md:79-80` links to hods-poc.netlify.app (unverified). — status: proposed
- 2026-10-12 `apps/docs/src/common/pages/design-and-content/content/content-style-guide.tsx` uses UK noun "dependant" correctly (a deliberate noun/adjective distinction); NOT a typo. `IHS` (Immigration Health Surcharge) is not a misspelling either. — status: dropped(false-positive)

## Outcome log
- 2026-10-12 docs-typos pass -> fork PR #8 https://github.com/olitreadwell/design-system-ukho/pull/8, branch `fix-documentation-typos`, base `master` (fork), 10 files, +18/-18. Fixes: `mutliple`->`multiple` (docs/working-on-your-project.md); `unecessary`->`unnecessary` (components/highlight/spec/Highlight.stories.mdx); `necesssary`->`necessary` (error-messages.tsx); `Visability`->`Visibility` (focus.tsx); `ot`->`of` "point 5 ot the government Service Standard" (leaders-guide.tsx); `Mulitple`->`Multiple` (operable.tsx); `calclulations`->`calculations` (understandable.tsx); `unecessary`->`unnecessary` and `infront`->`in front` (styles/images.tsx); `Technolgy`->`Technology` (styles/index.tsx); `agencey`->`agency`, `Carribean`->`Caribbean` x2, `emmisaries`->`emissaries`, `Africe`->`Africa` x2 (passport-details/enter-details.tsx). Found with a full-repo codespell sweep (codespell 2.4.3) plus manual review of every hit; each line re-verified on upstream master @ 358c818a. Verified locally with Node 24.21.0 + pnpm 12.3.4: `pnpm install` clean, `npm test` 190 passed / 8 skipped (22 suites), `tsc --noEmit` on apps/docs clean, MDX file still compiles.
