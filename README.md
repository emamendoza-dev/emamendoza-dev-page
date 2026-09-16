# emamendoza-dev-page

![Astro](https://img.shields.io/badge/Astro-7-FF5D01?style=flat-square&logo=astro&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-strict-3178C6?style=flat-square&logo=typescript&logoColor=white)
![pnpm](https://img.shields.io/badge/pnpm-managed-F69220?style=flat-square&logo=pnpm&logoColor=white)

Personal landing page and portfolio for Fernando Emanuel Mendoza Villar, built with [Astro](https://astro.build) and [Tailwind CSS 4](https://tailwindcss.com), bilingual in Spanish and English.

**🌐 Live site:** https://emamendoza-dev.github.io/emamendoza-dev-page/ (not yet deployed — Phase 5 of the roadmap)

## Quick start

### 1. Install pnpm and gitleaks

```sh
npm install -g pnpm
```

The pre-push hook scans for secrets with [gitleaks](https://github.com/gitleaks/gitleaks) 8.30.1 (the same version CI uses). Install the release binary and make sure `gitleaks` is on your `PATH`:

```sh
curl -sSfL https://github.com/gitleaks/gitleaks/releases/download/v8.30.1/gitleaks_8.30.1_linux_x64.tar.gz \
  | tar -xz -C ~/.local/bin gitleaks
gitleaks version
```

### 2. Clone and run

```sh
git clone git@github.com:emamendoza-dev/emamendoza-dev-page.git
cd emamendoza-dev-page
pnpm install   # also installs the pre-push hook
pnpm dev
```

## Workflow

| Branch        | Purpose                                | CI               | Protection                    |
| ------------- | -------------------------------------- | ---------------- | ----------------------------- |
| `development` | Integration branch for day-to-day work | No               | None                          |
| `main`        | Released state                         | On pull requests | PR with green checks required |

1. Branch from `development`: `git switch development && git switch -c feat/<topic>` (or `fix/`, `docs/`, `ci/`, `build/`, `chore/`), or commit directly on `development`.
2. Commit with Conventional Commits.
3. Push. The local pre-push hook runs `pnpm validate` and blocks the push if anything fails.
4. Merge topic branches into `development` freely (no CI).
5. When `development` is ready, open a pull request `development` → `main`. CI (`validate`, `secret-scan`) must pass before merging.

## Commands

| Command             | Description                              |
| ------------------- | ---------------------------------------- |
| `pnpm dev`          | Start the local dev server               |
| `pnpm build`        | Build the static site into `dist/`       |
| `pnpm preview`      | Preview the production build locally     |
| `pnpm check`        | Type-check with `astro check`            |
| `pnpm format`       | Format the codebase with Prettier        |
| `pnpm format:check` | Check formatting without writing changes |
| `pnpm secrets`      | Scan the git history with gitleaks       |
| `pnpm validate`     | Run every check above (pre-push hook)    |

## Repository layout

```
.
├── src/
│   ├── layouts/         # Shared page layouts
│   ├── pages/           # Routes (es at root, en under /en/)
│   └── styles/          # Global Tailwind stylesheet
├── public/              # Static assets served as-is
├── astro.config.mjs     # site/base, i18n and Tailwind config
├── .github/workflows/   # CI: validate.yml
├── .github/dependabot.yml
├── docs/ROADMAP.md      # Project roadmap and decisions
├── AGENTS.md            # Conventions for AI agents
└── CLAUDE.md            # Imports AGENTS.md for Claude Code
```

## Roadmap

This project moves in phases: repository bootstrap, content, design system, mockups, build, deploy, maintenance. See [docs/ROADMAP.md](docs/ROADMAP.md) for the full plan and decisions.
