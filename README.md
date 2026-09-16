# emamendoza-dev-page

![Astro](https://img.shields.io/badge/Astro-7-FF5D01?style=flat-square&logo=astro&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-strict-3178C6?style=flat-square&logo=typescript&logoColor=white)
![pnpm](https://img.shields.io/badge/pnpm-managed-F69220?style=flat-square&logo=pnpm&logoColor=white)

Personal landing page and portfolio for Fernando Emanuel Mendoza Villar, built with [Astro](https://astro.build) and [Tailwind CSS 4](https://tailwindcss.com), bilingual in Spanish and English.

**🌐 Live site:** https://emamendoza-dev.github.io/emamendoza-dev-page/ (not yet deployed — Phase 5 of the roadmap)

## Quick start

### 1. Install pnpm

```sh
npm install -g pnpm
```

### 2. Clone and run

```sh
git clone git@github.com:emamendoza-dev/emamendoza-dev-page.git
cd emamendoza-dev-page
pnpm install
pnpm dev
```

## Commands

| Command             | Description                              |
| ------------------- | ---------------------------------------- |
| `pnpm dev`          | Start the local dev server               |
| `pnpm build`        | Build the static site into `dist/`       |
| `pnpm preview`      | Preview the production build locally     |
| `pnpm check`        | Type-check with `astro check`            |
| `pnpm format`       | Format the codebase with Prettier        |
| `pnpm format:check` | Check formatting without writing changes |

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
