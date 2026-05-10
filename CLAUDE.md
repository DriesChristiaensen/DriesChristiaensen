# Project Context for Claude

This repository is a **static single-page personal portfolio** for Dries Christiaensen. No build step, no backend, no package manager — pure HTML/CSS/JS on top of the BootstrapMade "Personal" template, with vendored libraries under `assets/vendor/`.

## Read this first

**Always consult [`AI_COMPASS.md`](./AI_COMPASS.md) before making changes.** It is the authoritative guide for this project and contains:

- Repository layout and tech inventory
- Page structure of `index.html` and section conventions
- Styling conventions (CSS variables, fonts, backgrounds)
- JavaScript conventions (IIFE in `main.js`, helper utilities)
- Content model (skills, resume, portfolio items)
- Personal context and tone of voice
- Explicit Do / Don't rules for AI prompts
- A common-task recipe table
- A list of known dead/legacy code

If `AI_COMPASS.md` and this file ever conflict, `AI_COMPASS.md` wins — update it when project conventions change.

## Quick reminders

- Edit `index.html`, `assets/css/style.css`, and `assets/js/main.js` directly. Reload the browser to see changes.
- Do **not** introduce a build system, npm, bundler, framework, or backend.
- Reuse the CSS variables `--custom-light`, `--custom-dark`, `--custom-vivid` rather than hardcoding accent colors.
- When changing a skill percentage, update **both** `aria-valuenow` and the `.val` text.
- New portfolio items must carry the correct `filter-*` class matching `#portfolio-flters`.
- Always update `AI_COMPASS.md` when changes affect anything it documents (layout, conventions, content model, recipes, etc.).
- After completing changes, always ask the user whether the latest changes should be pushed to the git repo.
