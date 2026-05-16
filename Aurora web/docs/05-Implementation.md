# 05 — Implementation

## File map

```
/                                Project root
├── Aurora.html                   Working source (with Tweaks panel)
├── Aurora-review.html            Lean source (Tweaks stripped) — input to bundler
├── Aurora-standalone.html        Source with bundler thumbnail (full)
├── aurora.html                   Bundled — full, ~1.7 MB
├── aurora-mobile.html            Bundled — lean, ~557 KB (recommended for review)
├── styles.css                    All visual styles & tokens
├── image-slot.js                 Drop-target web component
├── tweaks-panel.jsx              Dev-only React Tweaks shell (excluded from lean bundle)
└── docs/                         V-Model artifacts
    ├── 00-V-Model.md
    ├── 01-Flow.md
    ├── 02-Requirements.md
    ├── 03-Design.md
    ├── 04-Test-Cases.md
    ├── 05-Implementation.md
    └── 06-Test.md
```

## Requirement → Implementation traceability

| Req   | Location                                                  | Notes                                                          |
|-------|-----------------------------------------------------------|----------------------------------------------------------------|
| R-001 | `Aurora.html` §`<section class="hero">`                   | clamp-sized H1, dual CTAs                                      |
| R-002 | `Aurora.html` §`<header class="nav">` + inline scroll script | `.scrolled` class toggled on scrollY > 24                  |
| R-003 | `Aurora.html` §`<section id="collections">` + `.tier*` in `styles.css` | Bordered grid via 1px background-line trick           |
| R-004 | `Aurora.html` §`<section id="gallery">` + `.gallery, .g-1…g-5` | 12-col grid with staggered margins                      |
| R-005 | `Aurora.html` §`<section id="craft">` + `.craft*`         | Sticky media column; `<ol class="craft-steps">`               |
| R-006 | `Aurora.html` §`<section id="story">` + `.story*`         | Founder signature in italic serif                              |
| R-007 | `Aurora.html` §`<section class="section tight">` (testimonials) | Three-column bordered grid                              |
| R-008 | `Aurora.html` §`<section class="cta">` + `.cta`           | Inverted ink-block; light-on-dark CTA inversion                |
| R-009 | `Aurora.html` §`<section id="faq">` + `.faq` & `<details>`| Native disclosure; custom plus/minus glyph                     |
| R-010 | `Aurora.html` §`<section id="newsletter">` + `.news*`     | Inline confirmation via `nextElementSibling.querySelector`     |
| R-011 | `Aurora.html` §`<footer class="foot">` + `.foot*`         | Brand, 3 nav columns, base caption                             |
| R-012 | `image-slot.js`                                           | `localStorage[id]` persistence                                 |
| R-013 | `Aurora.html` inline JSX, `styles.css` `[data-mood="…"]` rules | 4 palettes: Snow / Muse / Stone / Night                  |
| R-014 | `Aurora.html` inline JSX → `.style.fontStyle`             | `h1 em, h2 em` selector                                        |
| R-015 | `Aurora.html` inline JSX → `.style.display`               | Targets `.strip`                                               |
| R-016 | `Aurora-review.html` + `super_inline_html` bundler        | Inlines fonts, CSS, scripts                                    |
| N-001/002 | `styles.css` `@media (max-width:900px)` and `(max-width:480px)` | All multi-col layouts collapse                       |
| N-003 | Verified at last `done` call                              | "No console errors" reported                                   |

## Implementation notes

### Why static HTML (not React) for the main page
The page is content-led, has no per-piece dynamic data, and is shared as a standalone file with reviewers on phones. Static HTML survives bundling and runs without Babel-in-browser, which was the cause of the iOS splash-stuck bug.

### Bordered-grid trick
The tier and testimonial grids use a 1px gap on a `background: var(--line)` parent with `1px` border around it. Children paint over the gap so each cell shows a hairline border that never doubles. This avoids `border-collapse` headaches and gives clean phone collapse.

### Sticky craft media
`.craft-media { position: sticky; top: 96px; }` paired with a long `<ol>` makes the image hold while the user reads the steps. Disabled below 900px (`position: static`) because phone viewports are too short.

### Image slot persistence
`image-slot.js` keys each slot by its `id` attribute. Slots without an id work in-session but warn on persist. All slots in this page carry ids: `hero`, `tier-1..3`, `g-1..5`, `craft`, `story`.

### Two bundle variants
- **Full** (`aurora.html`) keeps the Tweaks panel — useful for an internal stakeholder who wants to flip palettes during review.
- **Lean** (`aurora-mobile.html`) strips Tweaks + Babel + React — required for reliable iOS Safari rendering.

## Build / export commands

| Action                                        | How                                                |
|-----------------------------------------------|----------------------------------------------------|
| Preview source                                | Open `Aurora.html`                                 |
| Update standalone (full)                       | Bundle `Aurora-standalone.html` → `aurora.html`    |
| Update standalone (lean / mobile)              | Bundle `Aurora-review.html` → `aurora-mobile.html` |
| Persist a Tweaks value                         | Toggle in panel → host rewrites `EDITMODE` block   |

## Known issues / debt

| Tag    | Item                                                                                           |
|--------|------------------------------------------------------------------------------------------------|
| DEBT-1 | Newsletter is form-only; not wired to a real ESP                                               |
| DEBT-2 | No image-alt text on `<image-slot>` drops (need authoring UX)                                  |
| DEBT-3 | `tweaks-panel.jsx` loads three big CDN scripts in full bundle — switch to local copies if size matters |
| DEBT-4 | No dark-mode automatic via `prefers-color-scheme`; Night is a manual mood only                 |
