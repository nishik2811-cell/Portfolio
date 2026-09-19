# Nishita Kumari — Portfolio

A personal developer portfolio for **Nishita Kumari**, a B.Tech student in Mathematics & Computing at Jaypee Institute of Information Technology. Built as a plain static site — no framework, no build step, no npm dependency required to run it.

## Live sections

The page is a single scroll experience, in this order:

1. **Hero** — name, tagline, and primary CTAs (Explore work / Resume)
2. **About** — a short personal statement plus a few quick facts
3. **Cinematic interlude** — a full-bleed breathing moment between About and Education
4. **Education** — JIIT (B.Tech, Mathematics & Computing), plus senior/secondary schooling
5. **Projects** — ARGUS, AQI Prediction, and this portfolio's own "Night World Edition" build
6. **Currently Working On** — SkillSwap, a co-authored research book chapter, and ongoing DSA/C++ practice
7. **Experience & Activities** — AIML Hub and DICE Hub at JIIT
8. **Tech Stack** — languages, frontend, data/ML, database, dev tools, and design tools
9. **Contact**

## Design & interaction

- A single persistent video (`frieren.mp4`) plays behind the whole page, muted/looped/autoplaying — it's never seeked or scrubbed. An `IntersectionObserver` swaps a `body[data-scene]` attribute as each section scrolls into view, which drives CSS-only crossfades on the overlay darkness and video brightness per section.
- Each section scales/fades in and out as it enters and leaves the viewport (a cinematic "depth" effect), implemented with the native `animation-timeline: view()` CSS API where supported, with a small JavaScript fallback (scroll + `requestAnimationFrame`) elsewhere.
- Small caption text (section numbers, eyebrows, stat labels) adapts its color to the video's live brightness, sampled from a tiny offscreen canvas.
- Project and "Currently Working On" cards become clickable links straight to their GitHub repo (or live demo) whenever one is set in `data.js`, and can optionally show a full, uncropped screenshot (`object-fit: contain`, so UI screenshots never get cut off at the edges).
- A custom trailing cursor, magnetic buttons, and mouse-reactive lighting are enabled only on fine-pointer (non-touch) devices.
- Respects `prefers-reduced-motion`: continuous animation and the custom cursor are disabled, entrance transitions become instant.
- Responsive down to small phone widths, including a landscape-phone-specific hero layout.

## Tech stack

Plain HTML, CSS, and JavaScript — no framework, no bundler, no npm packages required at runtime.

## Project structure

```
index.html    Page markup and section structure
styles.css    All styling, animation, and responsive rules
script.js     Content rendering, scroll/scene logic, cursor, interactions
data.js       All editable content (education, projects, experience, contact info)
frieren.mp4   Background video
assets/       Project/work screenshots referenced from data.js
```

## Editing content

Everything user-facing — education entries, project descriptions, tech stack items, experience, and contact links — lives in `data.js`. Edit the values there; nothing else needs to change. Each `projects` and `currentlyWorking` entry accepts an optional `image` (a path under `assets/`) and `github`/`demo` link — set either link and the whole card becomes clickable.

**Known placeholders still to fill in:**

- The book-chapter and DSA/C++ "Currently Working On" entries have no screenshot or link (no public repo/page to point to) — expected, not an oversight.

## Running locally

This is a static site, but the background-video brightness sampling uses `<canvas>` pixel reads, which browsers block on a `file://` origin. Serve the folder over a local HTTP server instead of opening `index.html` directly:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000` in your browser.
