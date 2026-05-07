# AI Compass — DriesChristiaensen Portfolio

A guidance document for AI assistants working on this codebase. Read this first before prompting changes.

---

## 1. What this project is

A **single-page personal portfolio website** for Dries Christiaensen (SAP Application Developer Consultant at Flexso Digital, Belgium). It is a static site — pure HTML/CSS/JS — built on top of the BootstrapMade "Personal" template (v4.7.0).

- **Purpose:** showcase CV, skills, and portfolio projects.
- **Audience:** recruiters, peers, clients.
- **Hosting:** static files; the entry point is `index.html` in the repo root.
- **No build step.** No package manager. No framework. No backend.

---

## 2. Repository layout

```
DriesChristiaensen/
├── index.html                  # Single page — all sections live here
├── assets/
│   ├── css/style.css           # ~1100 lines, single stylesheet (template + custom)
│   ├── js/main.js              # ~290 lines, IIFE — nav, isotope, typed, swiper, glightbox
│   ├── files/                  # CV PDFs (NL + EN) and SWOT
│   ├── img/                    # Backgrounds, favicons, profile photo
│   │   └── portfolio/          # Project screenshots (web*, app*, sap*)
│   └── vendor/                 # Vendored libs (no npm) — bootstrap, bootstrap-icons,
│                               #   boxicons, glightbox, isotope-layout, php-email-form,
│                               #   purecounter, remixicon, swiper, typed.js, waypoints
└── .vscode/
```

There is **no `package.json`, no `node_modules`, no bundler config**. All third-party code is committed under `assets/vendor/`.

---

## 3. Tech & libraries in use

| Concern         | Library                       | Where used                             |
|-----------------|-------------------------------|----------------------------------------|
| Layout/grid     | Bootstrap 5                   | `index.html` classes, `style.css`      |
| Icons           | bootstrap-icons, boxicons, remixicon, FontAwesome 5 (CDN) | Throughout `index.html`            |
| Hero typing     | typed.js                      | `.typed[data-typed-items]`             |
| Portfolio grid  | isotope-layout                | `.portfolio-container` + `#portfolio-flters` filters |
| Lightbox        | glightbox                     | `.portfolio-lightbox`                  |
| Skill bars      | waypoints                     | Animates `.progress-bar` on scroll     |
| Sliders         | swiper                        | Testimonials + portfolio details (currently unused in markup) |
| Counters        | purecounter                   | Loaded but not actively used           |
| Fonts           | Google Fonts (Open Sans, Raleway, Poppins) | CDN link in `<head>`     |

---

## 4. Page structure (`index.html`)

Sections, in order:

1. **`#header`** — name, typed tagline (`SAP Consultant, Web Developer, Youth Animator`), nav, profile/socials, CV download links (NL/EN).
2. **`#about`** — bio, programming skills (HTML/JS/CSS/Java/SQL/Python with `%` bars), interests grid, languages.
3. **`#resume`** — Summary, Education, Professional Experience.
4. **`#portfolio`** — Isotope-filtered grid (`All / Career / Web / App / SAP`) of project tiles with lightbox screenshots.
5. **Contact section** — present in source but **commented out**.
6. **Credits footer.**

### Navigation behavior (see `main.js`)
- Clicking a nav link adds `header-top` to `#header` (collapses hero), hides `#profile`, and toggles `section-show` on the target section.
- Mobile nav toggles `.navbar-mobile` and swaps `.bi-list` ↔ `.bi-x` on the toggle icon.
- Deep-linking via `window.location.hash` is supported on load.

### Portfolio filters (`#portfolio-flters`)
Filter classes used on `.portfolio-item`: `filter-job`, `filter-web`, `filter-app`, `filter-sap`. (`filter-card` is referenced in HTML comments but unused.)

---

## 5. Styling conventions

- **CSS variables** (`:root` in `style.css`):
  - `--custom-light: #A3CCEB`
  - `--custom-dark: #0c4374`
  - `--custom-vivid: #0072C7`
  Use these for any new accent color — do not hardcode hex values for the primary palette.
- **Fonts:** headings → Raleway / Poppins, body → Open Sans.
- **Backgrounds:** `bg1Mobile.jpg` for narrow viewports, `bg1.jpg` (fixed-attachment) for `min-width: 1024px`. Other `bg*.jpg` files exist as historical alternatives.
- All custom CSS lives in the single file `assets/css/style.css`. There is no preprocessor.

---

## 6. JavaScript conventions

- All custom JS is wrapped in an IIFE in `assets/js/main.js`.
- Helper utilities `select()`, `on()`, `toggleClass()`, `scrollto()` are defined at the top — reuse them rather than calling `document.querySelector` directly.
- Vendor scripts are loaded via `<script src="assets/vendor/...">` tags at the bottom of `index.html`. Order matters (vendors before `main.js`).
- The orphan `toggleDropdown()` at the bottom of `main.js` references `#resume-dropdown`, which does not exist in the current markup — it is dead code from a prior iteration.

---

## 7. Content / data model

There is no CMS or JSON data source. All content is **hand-edited HTML** in `index.html`:

- **Skills** are individual `.progress` blocks — change percent in **two** places (`.val` text and `aria-valuenow`).
- **Resume entries** are `.resume-item` blocks inside `.resume-section`.
- **Portfolio entries** are `.col-lg-4 .portfolio-item` blocks. Each must:
  - Carry the right `filter-*` class(es) for Isotope.
  - Reference an image in `assets/img/portfolio/` (naming: `<type>-<appId 3 digits>-<imgId 3 digits>.png`, e.g. `web-010-001.png`).
  - Use `data-gallery="portfolioGallery"` on lightbox links so glightbox groups them.
  - Include a `<ul class="portfolio-tags">` chip-list as a sibling of `.portfolio-wrap` (inside `.portfolio-item`), shown beneath the tile.
  - Mirror those tags in a `data-description="…"` attribute on each lightbox `<a>` so glightbox renders them as the subtle caption (separator: ` · `).
- **CV downloads** point at `assets/files/DriesChristiaensen_NL_CV.pdf` and `DriesChristiaensen_EN_CV.pdf` — replace those files in place when updating the CV.

---

## 8. Personal context (the human behind the site)

Useful when AI is asked to write copy, taglines, or new sections:

- **Name:** Dries Christiaensen — Zoersel, Belgium.
- **Education:** Bachelor in Applied Computer Sciences, UC Leuven-Limburg (2020–2024). Year of Civil Engineering at KU Leuven before switching.
- **Current role:** SAP Application Developer Consultant @ Flexso Digital, Kontich (since Oct 2024).
- **Prior role:** Junior Web Developer @ Adshot, Leuven (2023–2024).
- **Identity:** SAP Consultant + Web Developer + Youth Animator (Chiro). Sporty, social, music/guitar, snowboarding, cooking.
- **Languages:** NL (native), EN (high), FR (mid).
- **Tone of voice in existing copy:** first-person, warm, slightly informal, enthusiastic. Mixes career and personality. Keep that tone in any generated copy.

---

## 9. Compass for AI prompts

When asking an AI to modify this repo, follow these rules of thumb.

### Do
- Edit `index.html`, `assets/css/style.css`, and `assets/js/main.js` directly — no build step needed; reload the browser to see changes.
- Reuse the CSS variables (`--custom-vivid`, etc.) and existing class patterns (`section-title`, `resume-item`, `portfolio-item`, `progress`).
- Add new portfolio entries by **copying an existing `.portfolio-item` block** and adjusting image, filter classes, and text.
- Keep filter classes (`filter-web`, `filter-app`, `filter-sap`, `filter-job`) consistent with the buttons in `#portfolio-flters`.
- Keep the BootstrapMade attribution comment block unless a pro license is purchased — see template license note at the top of `index.html` and `style.css`.
- Update **both** `aria-valuenow` and the `.val` text when changing a skill percentage.
- Place new images under `assets/img/portfolio/` and follow the naming convention (`web*`, `app*`, `sap*`).
- Vendor any new library under `assets/vendor/<name>/` and add `<script>`/`<link>` tags before `main.js` / after `style.css`.

### Don't
- Don't introduce a build system, npm, bundler, or framework — this is intentionally a static site.
- Don't replace the vendored libraries with CDN links wholesale (FontAwesome is the only CDN currently); the project is meant to work offline / without external dependencies beyond fonts and FontAwesome.
- Don't add a backend, contact-form handler, or analytics without explicit instruction (the contact section is commented out on purpose).
- Don't break the IIFE wrapper in `main.js` — global leakage is avoided deliberately.
- Don't touch the BootstrapMade license header in template files unless removing the template entirely.
- Don't add new filter buttons without also tagging at least one `.portfolio-item` with that filter class (Isotope will silently filter to empty otherwise).
- Don't hardcode colors that already exist as CSS variables.

### Common tasks — quick recipe

| Task                          | Files to touch                                                  |
|-------------------------------|-----------------------------------------------------------------|
| Add a portfolio project       | `index.html` (new `.portfolio-item` + `.portfolio-tags` + `data-description`) + `assets/img/portfolio/` |
| Add a new portfolio category  | `index.html` `#portfolio-flters` + matching `filter-*` classes |
| Update CV PDFs                | Replace files in `assets/files/`                                |
| Tweak hero job titles         | `index.html` `<span class="typed" data-typed-items="…">`        |
| Update skill bar              | `index.html` — both `aria-valuenow` and `.val`                  |
| Change accent color           | `assets/css/style.css` — `:root` variables only                 |
| Restore contact section       | Uncomment `<!-- ======= Contact Section ======= -->` in `index.html` |
| Fix mobile nav bug            | `main.js` `.mobile-nav-toggle` handler + `style.css` `.navbar-mobile` rules |

---

## 10. Known dead/legacy code (safe to ignore or remove)

- `toggleDropdown()` in `main.js` — references missing `#resume-dropdown`.
- Commented `filter-card` portfolio items at the end of `#portfolio`.
- `.testimonials-slider` and `.portfolio-details-slider` Swiper inits — no markup uses them currently.
- `purecounter` script is loaded but no `.purecounter` elements exist.
- `php-email-form/validate.js` is loaded; only meaningful if the contact section is re-enabled.

If asked to "clean up" the site, these are the obvious candidates — but check with the user first, since they may be kept intentionally for quick re-enabling.

---

*Last compass update: 2026-05-06.*
