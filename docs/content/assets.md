# Asset direction and inventory

Visual, motion and audio direction for every image, animation and sound the site uses. Exact color hex values are defined in Phase 2 (`docs/design-system/tokens.md`); this document only sets direction.

## Master brief

Repeat this brief verbatim at the top of every generation prompt below.

> Google's design essence: simple, few elements with intent, lots of whitespace, color used only to guide attention, geometric shapes with purposeful motion. The subject is complex technology (AIoT, embedded systems, cloud, computer vision) told with human warmth, not cold or clinical.
>
> Concept: "from circuit to cloud." PCB traces reduced to lines and circular nodes — a node represents a sensor, a line represents a data flow — converging into cloud or dashboard shapes.
>
> Palette direction: deep blue base, electric green accent reserved for the "live signal" (active nodes, primary CTAs, active/success states), neutral grays for secondary text (a gray near `#636569` as a subtle nod to IPN, used sparingly). Exact hex values belong to Phase 2 tokens; do not hardcode a final palette from this brief.
>
> Signature motif: two phase-shifted signals travelling along the traces together — inspired by the interdisciplinary, two-offset-signals meaning behind the UPIITA-IPN logo. This is inspiration only: never reproduce, trace, or reference the UPIITA or IPN logo itself.

## Forbidden

Never generate or use:

- Third-party or institutional logos (including UPIITA/IPN).
- Real client data, dashboards, or screenshots.
- Glowing brains, humanoid robots, or generic "AI" clichés.
- Rainbow or oversaturated palettes.
- Stock-photo clichés (handshakes, generic "coder" stock photos, etc.).
- Autoplay sound of any kind.

## Inventory

| id  | Asset                         | Section          | Purpose                                                               | Format                               | Dimensions (indicative)   | Light/dark | Status  |
| --- | ----------------------------- | ---------------- | --------------------------------------------------------------------- | ------------------------------------ | ------------------------- | ---------- | ------- |
| A01 | Portrait                      | Hero             | Owner photo                                                           | JPEG/WebP                            | square, ≥ 800×800         | n/a        | pending |
| A02 | Hero visual                   | Hero             | Static circuit-to-cloud illustration                                  | SVG                                  | responsive, ~ 800×600     | both       | pending |
| A03 | Hero motion loop              | Hero             | Silent 5–8 s ambient loop of the signal motif                         | SVG/Lottie (MP4 only as last resort) | responsive                | both       | pending |
| A04 | Featured project cover        | Featured project | Lead visual for the road inspection platform                          | SVG/WebP                             | 16:9, ~ 1600×900          | both       | pending |
| A05 | Featured project screenshot 1 | Featured project | Synthetic UI screenshot, phone frame                                  | WebP/PNG                             | phone frame, ~ 390×844    | both       | pending |
| A06 | Featured project screenshot 2 | Featured project | Synthetic UI screenshot, browser frame                                | WebP/PNG                             | browser frame, ~ 1440×900 | both       | pending |
| A07 | Featured project screenshot 3 | Featured project | Synthetic UI screenshot (optional third)                              | WebP/PNG                             | phone or browser frame    | both       | pending |
| A08 | Tech icon set                 | Skills           | One consistent icon per technology                                    | SVG (Simple Icons)                   | 24×24 base                | both       | pending |
| A09 | UI/section icon set           | all sections     | Section markers, bullet icons, nav icons                              | SVG (Lucide)                         | 24×24 base                | both       | pending |
| A10 | "EM" monogram                 | favicon, OG      | Brand mark for favicon and Open Graph images                          | SVG → PNG/ICO                        | favicon 32×32/512×512     | both       | pending |
| A11 | OG image — es                 | meta             | Open Graph preview image, Spanish                                     | PNG/WebP                             | 1200×630                  | n/a        | pending |
| A12 | OG image — en                 | meta             | Open Graph preview image, English, same template                      | PNG/WebP                             | 1200×630                  | n/a        | pending |
| A13 | Sonic logo (optional)         | Hero or Contact  | 1–2 s electric-pulse-to-warm-tone sound, on explicit user action only | MP3/OGG                              | ~ 1–2 s                   | n/a        | pending |

## Alt text and generation prompts

### A02 — Hero visual

- Alt (es): "Ilustración de trazos de circuito convergiendo en una nube, representando el paso de hardware a software."
- Alt (en): "Illustration of circuit traces converging into a cloud, representing the path from hardware to software."
- Prompt: "Minimalist geometric illustration in the Google-essence master brief style above. PCB traces as thin lines with circular nodes flowing left to right into a soft cloud/dashboard silhouette. Deep blue base, one electric-green accent line showing an active signal, generous whitespace, no text, no logos."

### A03 — Hero motion loop

- Alt (es): "Animación silenciosa y breve de dos señales desfasadas viajando por los trazos del circuito hacia la nube." (decorative; expose as `aria-hidden` if purely ambient, per Phase 4 accessibility spec)
- Alt (en): "Short silent animation of two phase-shifted signals travelling along the circuit traces toward the cloud."
- Prompt: "Same circuit-to-cloud scene as the hero visual, animated as a seamless 5–8 second loop. Two phase-shifted pulses (signature motif) travel together along the traces toward the cloud shape, one always slightly offset from the other. Subtle, restrained motion — no camera shake, no fast cuts. Silent. Must degrade gracefully to the static A02 illustration when `prefers-reduced-motion` is set."

### A04 — Featured project cover

- Alt (es): "Composición sintética que representa una plataforma de inspección vial: mapa de carreteras y panel de detección."
- Alt (en): "Synthetic composition representing a road-inspection platform: a road map and a detection dashboard."
- Prompt: "Abstract, synthetic composition (never real data) suggesting a road-inspection IoT platform: a stylized road/map line, a few sensor nodes, and a dashboard panel, in the circuit-to-cloud visual language of the master brief. No real screenshots, no client branding."
- Path: `images/featured-project/cover.svg` (base-relative, resolved via `import.meta.env.BASE_URL`; used in `docs/content/{es,en}/04-featured-project.md`).

### A05–A07 — Featured project screenshots (device-framed)

- Alt (es), phone: "Captura sintética de la app móvil de inspección, dentro de un marco de teléfono."
- Alt (en), phone: "Synthetic screenshot of the inspection mobile app, inside a phone frame."
- Alt (es), browser: "Captura sintética del panel web de operación, dentro de un marco de navegador."
- Alt (en), browser: "Synthetic screenshot of the web operations panel, inside a browser frame."
- Prompt: "Fictional, synthetic UI mockup (no real client data) of a road-inspection app screen / operations dashboard, styled with the circuit-to-cloud palette and generous whitespace, placed inside a generic phone or browser device frame. No real logos, no real place names tied to a client."
- Path (A05, phone): `images/featured-project/screenshot-mobile.webp` (base-relative; used in `docs/content/{es,en}/04-featured-project.md`).
- Path (A06, browser): `images/featured-project/screenshot-web.webp` (base-relative; used in `docs/content/{es,en}/04-featured-project.md`).
- Path (A07): not referenced by any section; no path assigned (optional, unused).

### A08 — Tech icon set

- Alt (es/en): per-technology, e.g. "Ícono de TypeScript" / "TypeScript icon".
- Prompt: "Use the Simple Icons set as-is (single consistent style, no custom redraws) for each technology named in the Skills section."

### A09 — UI/section icon set

- Alt (es/en): per-icon, functional label, e.g. "Ícono de contacto por correo" / "Email contact icon".
- Prompt: "Use the Lucide icon set as-is, single stroke weight matched to the signature motif's line weight, deep blue or neutral gray fill depending on theme."

### A10 — "EM" monogram

- Alt (es): "Monograma EM, marca personal del sitio."
- Alt (en): "EM monogram, the site's personal mark."
- Prompt: "Minimalist geometric monogram combining the letters E and M, built from the same line-and-node visual language as the circuit motif. Must read clearly at 32×32 px. Deep blue on light background, light on dark background."

### A11/A12 — OG images (es/en)

- Alt: OG images are metadata, not rendered inline; no visible alt text, but include an accessible `og:image:alt` — (es) "Fernando Emanuel Mendoza Villar, Ingeniero en Mecatrónica y Desarrollador Full Stack AIoT." / (en) "Fernando Emanuel Mendoza Villar, Mechatronics Engineer and Full Stack AIoT Developer."
- Prompt: "Same template for both locales: circuit-to-cloud motif on the left third, name and headline as the only text on the right two-thirds, in the section's target locale. Deep blue background, electric green accent line, generous margins, 1200×630."

### A13 — Sonic logo (optional)

- Prompt: "A 1–2 second sound: a short electric pulse/click opening into one warm, resolved tone — no jingle, no melody. Must never autoplay and must never accompany routine UI interactions (clicks, hovers, form states)."

## Motion and audio rules

- Every animation loop is silent by default; the hero motion loop (A03) carries no audio track.
- Any animation must respect `prefers-reduced-motion` and fall back to its static equivalent (e.g. A03 falls back to A02).
- The hero motion loop must not degrade Lighthouse Performance below 95; prefer a lightweight SVG/Lottie animation over MP4/video.
- No sound plays automatically on page load, scroll, or routine navigation.
- The optional sonic logo (A13) plays only on an explicit, discrete user action (e.g. a dedicated "play" control), never as a UI feedback sound (clicks, toggles, form validation, etc.), and never loops.
