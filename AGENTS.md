# AGENTS.md

Instructions for AI agents editing this repository. Human-facing setup lives in `README.md`; the project plan and decisions live in `docs/ROADMAP.md`.

## What this repo is

The personal landing page and portfolio of Fernando Emanuel Mendoza Villar, built with Astro and Tailwind CSS 4, bilingual (Spanish/English). Work moves in phases documented in `docs/ROADMAP.md`; check it before starting new work.

## Verify every change

```sh
pnpm validate
```

It runs `format:check`, `check`, `build` and a gitleaks history scan, and must exit 0. The same command runs as a pre-push hook; never bypass it (`--no-verify`, `SKIP_SIMPLE_GIT_HOOKS=1`).

## Branch workflow

- `main` is protected. Never commit to it directly; work on a branch named `<type>/<topic>` using Conventional Commit types.
- Changes reach `main` only through a pull request with the `validate` and `secret-scan` checks green.
- CI runs on pull requests only; local validation is the first gate.

## Language

- Site content (copy rendered on the page, in `src/`) is written in **both Spanish and English**, with Spanish (`es`) as the default locale at the root and English under `/en/`.
- Repository docs, code comments, commit messages and configuration are **English**.
- Commits follow Conventional Commits (`feat:`, `fix:`, `docs:`, `ci:`, `build:`, `chore:`). No AI attribution.

## Base path rule

This site deploys to a GitHub Pages project site under `base: '/emamendoza-dev-page'` (see `astro.config.mjs`). Every internal link and static asset reference must be built through `import.meta.env.BASE_URL`. Never hardcode a root-relative path (e.g. `/en/`, `/favicon.svg`) — it breaks once the site is served from a subpath.

## Privacy and confidentiality

This repository is **public**. Never publish, in code, comments, content, commit messages or docs:

- The owner's personal phone number.
- Confidential client names, or any other detail covered by a confidentiality agreement — describe past work generically (e.g. "a clinic network", "a road infrastructure agency").
- Internal system names, table or topic names, hostnames, IP addresses, or internal authentication mechanisms.

These rules mirror `emamendoza-dev-cv/AGENTS.md` (the private CV repository, source of truth for experience and project content). When importing content from that repo or from the profile README, re-apply this privacy pass before publishing it here.
