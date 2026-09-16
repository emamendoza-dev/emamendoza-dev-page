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

## Context

The `dev/` workspace already holds two related repositories. This project reuses their content and conventions instead of reinventing them.

| Repository            | Visibility | Role for this project                                                                                                                                                   |
| --------------------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `emamendoza-dev`      | Public     | GitHub profile README. Source for stack, featured projects and tagline.                                                                                                 |
| `emamendoza-dev-cv`   | Private    | CV as code (RenderCV YAML). Source of truth for experience, projects, education, skills. Reference for repo conventions (`AGENTS.md`, CI, Dependabot, release runbook). |
| `emamendoza-dev-page` | To create  | This landing page.                                                                                                                                                      |

**Privacy rule inherited from the CV repo:** the CV contains a personal phone number and confidential client details are described generically. The public site must never publish the phone number, and must follow the same confidentiality rules as `emamendoza-dev-cv/AGENTS.md`.

## Decisions

| ID  | Decision                     | Status                       | Resolution                                                                                                                                                              | Blocks           |
| --- | ---------------------------- | ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| D1  | Hosting target               | Decided (2026-09-16)         | GitHub Pages, free plan, deployed with GitHub Actions                                                                                                                   | Phase 0, Phase 5 |
| D2  | Public URL                   | Decided (2026-09-16)         | Project site `https://emamendoza-dev.github.io/emamendoza-dev-page` (Astro `base: '/emamendoza-dev-page'`). Custom domain reconsidered later; it would drop the `base`. | Phase 0, Phase 5 |
| D3  | Repo visibility              | Decided (2026-09-16)         | Public (required by free GitHub Pages). A sensitive-data check runs before the first push and on every PR.                                                              | Phase 0          |
| D4  | Site language                | Decided (2026-09-16)         | Bilingual Spanish/English with Astro i18n routing                                                                                                                       | Phase 1, Phase 2 |
| D5  | Styling approach             | Decided (2026-09-16)         | Tailwind CSS 4, design tokens as `@theme` variables                                                                                                                     | Phase 2, Phase 4 |
| D6  | Content sync with CV         | Open, reviewed after Phase 0 | Manual copy into content collections · build-time import of the CV YAML (the CV repo is private, so import needs a sanitized export)                                    | Phase 1, Phase 6 |
| D7  | Package manager              | Decided (2026-09-16)         | pnpm                                                                                                                                                                    | Phase 0          |
| D8  | Default locale and URL shape | Decided (2026-09-16)         | `es` at root, English under `/en/`                                                                                                                                      | Phase 1, Phase 4 |

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
- [ ] Create the public remote with `gh repo create emamendoza-dev/emamendoza-dev-page --public --source . --push` and set description/topics.
- [ ] Enable GitHub secret scanning and push protection on the repo.
- [x] CI `validate.yml`: pnpm install, `astro check`, build, secret scan on push/PR.
- [x] `dependabot.yml` for `npm` (pnpm lockfile) and `github-actions`.
- [x] Conventional Commits, no AI attribution.

**Exit:** `pnpm build` passes locally and the first CI run is green.

## Phase 1 — Content inventory

**Goal:** know exactly what the site says before designing how it looks.

- [x] Resolve D4 and D8.
- [ ] Resolve D6.
- [ ] Write copy in both Spanish and English.
- [ ] Define site sections: Hero, About, Experience, Featured projects, Skills/stack, Education & certifications, Contact.
- [ ] Extract copy from the profile README and CV YAML into `docs/content/`.
- [ ] Rewrite for web (shorter than the CV; outcome-first).
- [ ] List assets needed: photo, project screenshots, logos/icons, CV download link strategy (the CV release is private).
- [ ] Privacy pass: no phone, no confidential names.

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
- [ ] Optional: automate sync if D6 chose build-time import.
- [ ] Dependabot PRs reviewed monthly.

## Environment notes

| Tool  | Status (2026-09-16)                                                                                         |
| ----- | ----------------------------------------------------------------------------------------------------------- |
| Node  | 26.8.2 (Homebrew)                                                                                           |
| npm   | 11.19.1                                                                                                     |
| Astro | 7.3.3 latest (`create-astro` 5.2.4)                                                                         |
| gh    | 2.101.0, authenticated as `emamendoza-dev` (SSH)                                                            |
| pnpm  | Not installed yet (decided in D7). Corepack is no longer bundled with Node 25+, so install pnpm standalone. |
