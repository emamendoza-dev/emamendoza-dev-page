# Roadmap — emamendoza-dev-page

Personal landing page and portfolio for Fernando Emanuel Mendoza Villar, built with Astro and hosted from GitHub. Work moves in phases: repository first, then design system, then mockups, then implementation. Each phase ends with a verifiable exit criterion before the next one starts.

## Quick path

| #   | Phase                | Output                                   | Exit criterion                               |
| --- | -------------------- | ---------------------------------------- | -------------------------------------------- |
| 0   | Repository bootstrap | GitHub repo, Astro skeleton, base config | `pnpm build` passes locally and in CI        |
| 1   | Content inventory    | `docs/content/` source of truth          | Every section has approved copy              |
| 2   | Design system        | `docs/design-system/*.md`                | Tokens and components specified              |
| 3   | Mockups              | `docs/mockups/*.md`                      | Every page/section has an approved wireframe |
| 4   | Build                | Astro components and pages               | Mockups implemented, checks green            |
| 5   | Deploy               | Public site                              | Site live, Lighthouse targets met            |
| 6   | Maintenance          | Automation                               | Content sync and updates documented          |

## Status

**Current phase:** Phase 2 — Design system (not started). Last updated 2026-09-19.

| Phase                    | State          |
| ------------------------ | -------------- |
| 0 — Repository bootstrap | Done           |
| 1 — Content inventory    | Done           |
| 2 — Design system        | Ready to start |
| 3–6                      | Not started    |

### Done so far

| Area       | Result                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Repository | Public `emamendoza-dev/emamendoza-dev-page`, description, topics                                                                                                                                                                                                                                                                                                                                                                                                              |
| Project    | Astro 7.3.3, Tailwind CSS 4.3.3, TypeScript strict (5.9.3), pnpm 12.4.2, `base: /emamendoza-dev-page`, i18n `es` root + `/en/` placeholder pages                                                                                                                                                                                                                                                                                                                              |
| Local gate | `pnpm validate` (format, `astro check`, build, gitleaks) as a pre-push hook                                                                                                                                                                                                                                                                                                                                                                                                   |
| CI         | `validate` + `secret-scan` on pull requests only                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Branches   | `development` for free work (no CI); `main` requires a PR with both checks green; applies to admins; no force push or deletion                                                                                                                                                                                                                                                                                                                                                |
| Security   | Secret scanning, push protection and Dependabot alerts enabled; Dependabot version updates monthly, TypeScript majors ignored                                                                                                                                                                                                                                                                                                                                                 |
| Decisions  | D1–D9 all decided                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Content    | Seven sections (Hero, About, Experience, Featured project, Skills, Education & certifications, Contact) with bilingual (es/en) copy, all approved (`docs/content/`). Employers named (already public via the profile README); confidential clients described generically. Media assets specified in `docs/content/assets.md`, not yet produced. CV download wired to per-locale placeholder stub PDFs in `public/cv/`; the real CV is generated later in the private CV repo. |

### Ready for Phase 2

- No open decisions block it: D1–D9 are all decided, and Phase 1 settled the content itself.
- Input: the approved copy under `docs/content/` and the art direction in `docs/content/assets.md`.
- Phase 2 owns the design tokens the content deliberately left out — exact hex values for the deep blue base, the electric green accent and the grays, plus type scale and spacing.
- Two rendering constraints inherited from Phase 1: Skills renders 36 chips across six groups, and the full UPIITA institution name is long for a heading, so plan a short form.

### Known follow-ups

- Dependabot security updates (automatic fix PRs) are disabled; alerts are on.
- Remove the TypeScript major ignore in `.github/dependabot.yml` once `@astrojs/check` supports TypeScript 7.
- `homepage` points to the Pages URL, which returns 404 until Phase 5.
- Media assets (photo, illustrations, screenshots, icons) are specified in `docs/content/assets.md` but not yet produced; Phase 4 needs the actual files before build.

## Context

The `dev/` workspace already holds two related repositories. This project reuses their content and conventions instead of reinventing them.

| Repository            | Visibility | Role for this project                                                                                                                                                   |
| --------------------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `emamendoza-dev`      | Public     | GitHub profile README. Source for stack, featured projects and tagline.                                                                                                 |
| `emamendoza-dev-cv`   | Private    | CV as code (RenderCV YAML). Source of truth for experience, projects, education, skills. Reference for repo conventions (`AGENTS.md`, CI, Dependabot, release runbook). |
| `emamendoza-dev-page` | Public     | This landing page.                                                                                                                                                      |

**Privacy rule inherited from the CV repo:** the CV contains a personal phone number and confidential client details are described generically. The public site must never publish the phone number, and must follow the same confidentiality rules as `emamendoza-dev-cv/AGENTS.md`.

## Decisions

| ID  | Decision                     | Status               | Resolution                                                                                                                                                                                                                                                            | Blocks           |
| --- | ---------------------------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| D1  | Hosting target               | Decided (2026-09-16) | GitHub Pages, free plan, deployed with GitHub Actions                                                                                                                                                                                                                 | Phase 0, Phase 5 |
| D2  | Public URL                   | Decided (2026-09-16) | Project site `https://emamendoza-dev.github.io/emamendoza-dev-page` (Astro `base: '/emamendoza-dev-page'`). Custom domain reconsidered later; it would drop the `base`.                                                                                               | Phase 0, Phase 5 |
| D3  | Repo visibility              | Decided (2026-09-16) | Public (required by free GitHub Pages). A sensitive-data check runs before the first push and on every PR.                                                                                                                                                            | Phase 0          |
| D4  | Site language                | Decided (2026-09-16) | Bilingual Spanish/English with Astro i18n routing                                                                                                                                                                                                                     | Phase 1, Phase 2 |
| D5  | Styling approach             | Decided (2026-09-16) | Tailwind CSS 4, design tokens as `@theme` variables                                                                                                                                                                                                                   | Phase 2, Phase 4 |
| D6  | Content sync with CV         | Decided (2026-09-16) | Manual copy into bilingual content collections with Zod schemas. The CV repo is a reference, not a build input: no tokens, no risk of publishing private fields. When the CV changes, review the site. A local `pnpm sync:cv` draft generator is optional in Phase 6. | Phase 1, Phase 6 |
| D7  | Package manager              | Decided (2026-09-16) | pnpm                                                                                                                                                                                                                                                                  | Phase 0          |
| D8  | Default locale and URL shape | Decided (2026-09-16) | `es` at root, English under `/en/`                                                                                                                                                                                                                                    | Phase 1, Phase 4 |
| D9  | Development workflow         | Decided (2026-09-16) | Work on `development` (no CI) or topic branches off it; release to protected `main` via PR from `development` with CI. Local `pnpm validate` runs as a pre-push hook.                                                                                                 | All phases       |

**Base path rule (D2):** every internal link and asset must go through `import.meta.env.BASE_URL`. Hardcoded `/...` paths break on the project site.

## Phase 0 — Repository bootstrap

**Goal:** an empty but production-shaped Astro project on GitHub.

- [x] Resolve D1, D2, D3, D7.
- [x] Install pnpm and pin it with `packageManager` in `package.json`.
- [x] `git init` with `main` as default branch.
- [x] Scaffold Astro (`pnpm create astro@latest`, minimal template, TypeScript strict).
- [x] Add Tailwind CSS 4 (`pnpm astro add tailwind`).
- [x] `.gitignore`: `node_modules/`, `dist/`, `.astro/`, `.env*`, `odd/`, `.atl/`, `.codegraph/`.
- [x] `.nvmrc` / `engines` pinning the Node version.
- [x] `astro.config.mjs` with `site` (and `base` if D2 requires it).
- [x] Tooling: Prettier (+ `prettier-plugin-astro`), `astro check`.
- [x] `README.md`, `AGENTS.md` + `CLAUDE.md` (`@AGENTS.md`), mirroring the CV repo.
- [x] Sensitive-data check before the first push: secret scan (e.g. gitleaks) over the tree and history, and a manual pass for phone, confidential client names and internal systems.
- [x] Create the public remote with `gh repo create emamendoza-dev/emamendoza-dev-page --public --source . --push` and set description/topics.
- [x] Enable GitHub secret scanning and push protection on the repo.
- [x] CI `validate.yml`: pnpm install, `astro check`, build, secret scan (on pull requests only since D9).
- [x] `dependabot.yml` for `npm` (pnpm lockfile) and `github-actions`.
- [x] Conventional Commits, no AI attribution.

**Exit:** `pnpm build` passes locally and the first CI run is green.

## Phase 1 — Content inventory

**Goal:** know exactly what the site says before designing how it looks.

- [x] Resolve D4, D6 and D8.
- [x] Write copy in both Spanish and English.
- [x] Define site sections: Hero, About, Experience, Featured projects, Skills/stack, Education & certifications, Contact.
- [x] Extract copy from the profile README and CV YAML into `docs/content/`.
- [x] Rewrite for web (shorter than the CV; outcome-first).
- [x] List assets needed: photo, project screenshots, logos/icons, CV download link strategy (the CV release is private).
- [x] Privacy pass: no phone, no confidential names.

**Exit:** content approved by the owner.

## Phase 2 — Design system (Markdown specs)

**Goal:** a token-based specification that both mockups and code consume.

Files under `docs/design-system/`:

| File               | Contents                                                                                                                        |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| `README.md`        | Principles, brand direction (mechatronics + software + AIoT)                                                                    |
| `tokens.md`        | Color (light/dark), typography scale, spacing, radii, shadows, motion, breakpoints                                              |
| `components.md`    | Atoms → molecules → organisms (atomic design): Button, Badge, Link, Card, SectionHeader, ProjectCard, TimelineItem, Nav, Footer |
| `accessibility.md` | Contrast targets (WCAG 2.2 AA), focus states, reduced motion                                                                    |

- [x] Resolve D5.
- [ ] Define tokens with names that map 1:1 to Tailwind 4 `@theme` variables.
- [ ] Specify each component: purpose, variants, states, tokens used.

**Exit:** tokens and components specified and approved.

## Phase 3 — Mockups (Markdown, for Claude Code Design)

**Goal:** wireframes precise enough to generate visual designs with Claude Code Design.

Files under `docs/mockups/`:

- [ ] `home.md` — section order, layout per breakpoint (mobile / tablet / desktop), components per section, referencing design-system names.
- [ ] One file per extra page if any (e.g. `project-detail.md`, `404.md`).
- [ ] Run the specs through Claude Code Design; store the approved result links or exports next to each spec.

**Exit:** every page has an approved mockup.

## Phase 4 — Build

**Goal:** implement the mockups in Astro, component by component.

- [ ] Tokens → Tailwind 4 `@theme` in the global stylesheet.
- [ ] i18n routing (es/en) per D8, with a language switcher.
- [ ] Content collections with Zod schemas for experience, projects, certifications.
- [ ] Components following the design-system hierarchy; presentational components receive data via props.
- [ ] Pages and layouts; SEO (meta, Open Graph, `sitemap`, `robots.txt`); favicon.
- [ ] Dark mode, responsive, reduced motion.
- [ ] Tests: `astro check` + Playwright smoke and accessibility checks (axe).

**Exit:** all mockups implemented; CI green.

## Phase 5 — Deploy

- [ ] Deploy workflow with `withastro/action` and `actions/deploy-pages`; set Pages source to GitHub Actions.
- [ ] Verify links and assets resolve under `/emamendoza-dev-page/`.
- [ ] Later (optional): custom domain, which removes `base`.
- [ ] Lighthouse targets: Performance ≥ 95, Accessibility 100, Best Practices 100, SEO 100.
- [ ] Link the site from the GitHub profile README and LinkedIn.

**Exit:** site live at the chosen URL.

## Phase 6 — Maintenance

- [ ] Document the content update flow (CV change → site change).
- [ ] Optional: local `pnpm sync:cv` script that drafts Spanish content from `../emamendoza-dev-cv` (D6), only if manual drift becomes a problem.
- [ ] Dependabot PRs reviewed monthly.

## Environment notes

| Tool     | Status (2026-09-16)                                                                                                                         |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| Node     | 26.8.2 (Homebrew)                                                                                                                           |
| npm      | 11.19.1                                                                                                                                     |
| Astro    | 7.3.3 (`create-astro` 5.2.4)                                                                                                                |
| gh       | 2.101.0, authenticated as `emamendoza-dev` (SSH)                                                                                            |
| pnpm     | 12.4.2, installed with `npm i -g pnpm` (no Corepack with Homebrew Node). Build scripts are approved in `pnpm-workspace.yaml` `allowBuilds`. |
| gitleaks | 8.30.1 in `~/.local/bin`, same version as CI                                                                                                |
