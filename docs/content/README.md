# Content source of truth

`docs/content/` is the approved bilingual copy for every site section. Phase 4 moves each file into an Astro content collection with a Zod schema; the field tables below are a sketch of that future schema, not a spec.

Sources: the public profile (`emamendoza-dev/README.md`) and the private CV (`emamendoza-dev-cv/Fernando_Emanuel_Mendoza_Villar_CV.yaml`, reference only, never a build input). Apply the privacy pass in [Privacy rules](#privacy-rules) whenever content moves from either source into this folder.

## Layout

```
docs/content/
├── es/
│   ├── 01-hero.md
│   ├── 02-about.md
│   ├── 03-experience.md
│   ├── 04-featured-project.md
│   ├── 05-skills.md
│   ├── 06-education.md
│   └── 07-contact.md
└── en/
    └── (same seven files)
```

Section order is fixed: `01-hero`, `02-about`, `03-experience`, `04-featured-project`, `05-skills`, `06-education`, `07-contact`. One file per section per locale.

## Frontmatter conventions

Common fields on every file:

| Field       | Type                                 | Notes                            |
| ----------- | ------------------------------------ | -------------------------------- |
| `section`   | string                               | one of the seven section slugs   |
| `locale`    | `es` \| `en`                         |                                  |
| `order`     | number                               | matches the `NN` filename prefix |
| `status`    | `draft` \| `in-review` \| `approved` |                                  |
| `updatedAt` | date (`YYYY-MM-DD`)                  |                                  |

Per-section fields (indicative sketch for the Phase 4 Zod schema — field names and shapes may change during implementation):

| Section          | Fields (sketch)                                                                          |
| ---------------- | ---------------------------------------------------------------------------------------- |
| Hero             | `name`, `role`, `tagline`, `summary`, `primaryCta {label, href}`, `cvCta {label, cvUrl}` |
| About            | `pillars[] {title, description, icon}`                                                   |
| Experience       | `entries[] {organization, role, location, start, end \| present, highlights[], stack[]}` |
| Featured project | `title, context, period, role, problem, solution, outcomes[], stack[], media[]`          |
| Skills           | `groups[] {label, items[]}`                                                              |
| Education        | `degrees[]`, `certifications[] {name, issuer, date}`                                     |
| Contact          | `channels[] {type: email \| linkedin \| github, label, href}`                            |

## Voice guide

- First person, formal, neutral Spanish: no regionalisms, no _voseo_/_tuteo_ slang.
- Outcome-first: lead with the result, then the mechanism.
- Short sentences over long compound ones.
- Quantify results whenever the source (README or CV) provides a number; never invent one.
- English copy is an adaptation, not a literal translation — it should read naturally to an English-speaking hiring audience while preserving the same facts and tone.

## es ↔ en glossary

Recurring terms that must translate consistently across sections:

| es                                       | en                               |
| ---------------------------------------- | -------------------------------- |
| Ingeniero en Mecatrónica                 | Mechatronics Engineer            |
| Desarrollador Full Stack                 | Full Stack Developer             |
| Especialista AIoT                        | AIoT Specialist                  |
| AIoT                                     | AIoT                             |
| plataforma multitenant                   | multitenant platform             |
| visión por computadora en el dispositivo | on-device computer vision        |
| inspección vial                          | road inspection                  |
| red de clínicas                          | clinic network                   |
| data warehouse                           | data warehouse                   |
| modelo dimensional                       | dimensional model                |
| Scrum Master                             | Scrum Master                     |
| arquitectura de microservicios           | microservices architecture       |
| pipeline geoespacial                     | geospatial pipeline              |
| hardware embebido                        | embedded hardware                |
| agentes de IA                            | AI agents                        |
| autenticación centralizada (SSO)         | centralized authentication (SSO) |
| protocolos industriales                  | industrial protocols             |

## Privacy rules

Mirrors `AGENTS.md`. Never publish:

- The owner's personal phone number.
- Confidential client names, or any detail covered by a confidentiality agreement — describe past work generically (e.g. "a clinic network", "a road infrastructure agency").
- Internal system names, table or topic names, hostnames, IP addresses, or internal authentication mechanisms.

## CV download

The Hero and Contact sections reference a `cvUrl` per locale:

| Locale | `cvUrl`        | Status           |
| ------ | -------------- | ---------------- |
| es     | `cv/cv-es.pdf` | Placeholder stub |
| en     | `cv/cv-en.pdf` | Placeholder stub |

Both files are one-page placeholder PDFs under `public/cv/`, checked in now so the download link and build wiring exist. The real, protected CV is generated later in the private `emamendoza-dev-cv` repository and dropped in by replacing these two files — no code change needed. The CV currently exists only in Spanish; an English version is planned but not yet written, so `cv-en.pdf` stays a placeholder until then.

`cvUrl` values are base-relative paths (no leading slash) and are resolved through `import.meta.env.BASE_URL` at build time, per the base path rule in `AGENTS.md` — never hardcode `/cv/...`.

## Approval table

All sections start `pending`. Update this table as copy moves through `draft` → `in-review` → `approved` (see [Frontmatter conventions](#frontmatter-conventions) for the per-file `status` field).

| Section             | es       | en       |
| ------------------- | -------- | -------- |
| 01 Hero             | approved | approved |
| 02 About            | approved | approved |
| 03 Experience       | approved | approved |
| 04 Featured project | approved | approved |
| 05 Skills           | approved | approved |
| 06 Education        | approved | approved |
| 07 Contact          | approved | approved |
