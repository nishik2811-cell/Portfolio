# Nishita Kumari — Portfolio

A personal developer portfolio for **Nishita Kumari**, a B.Tech student in Mathematics & Computing at Jaypee Institute of Information Technology. Built as a plain static site — no framework, no build step, no npm dependency required to run it.

## Live sections

The page is a single scroll experience, in this order:

1. **Hero** — name, tagline, and primary CTAs (Explore work / Resume)
2. **About** — a short statement plus a few quick facts
3. **Cinematic interlude** — a full-bleed breathing moment between About and Education
4. **Education** — academic background
5. **Projects** — ARGUS, AQI Predictor, Sanchay
6. **Currently Working On** — Amrosia, Sanchay, and ongoing DSA/C++ practice
7. **Experience & Activities**
8. **Tech Stack** — languages, AI/ML tools, and development tools
9. **Contact**

## Design & interaction

- A single persistent video (`frieren.mp4`) plays behind the whole page, muted/looped/autoplaying — it's never seeked or scrubbed. An `IntersectionObserver` swaps a `body[data-scene]` attribute as each section scrolls into view, which drives CSS-only crossfades on the overlay darkness and video brightness per section.
- Each section scales/fades in and out as it enters and leaves the viewport (a cinematic "depth" effect), implemented with the native `animation-timeline: view()` CSS API where supported, with a small JavaScript fallback (scroll + `requestAnimationFrame`) elsewhere.
- Small caption text (section numbers, eyebrows, stat labels) adapts its color to the video's live brightness, sampled from a tiny offscreen canvas.
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
```

## Editing content

Everything user-facing — education entries, project descriptions, tech stack items, experience, and contact links — lives in `data.js`. Edit the values there; nothing else needs to change.

**Known placeholders still to fill in:**

- `resumeUrl` in `data.js` points to `resume.pdf` — drop your actual resume PDF in the project root at that filename to make the "Resume" links work.
- CGPA and secondary-school details in `education` are placeholders.
- `contact.email`, `contact.github`, and `contact.linkedin` are placeholders.
- Several `experience` entries (company/hackathon/organization names) are placeholders pending real details.

## Running locally

This is a static site, but the background-video brightness sampling uses `<canvas>` pixel reads, which browsers block on a `file://` origin. Serve the folder over a local HTTP server instead of opening `index.html` directly:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000` in your browser.
