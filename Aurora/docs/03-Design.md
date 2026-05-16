# 03 — Design

## 1. Architecture

A single, static HTML document with one external stylesheet and two scripts. No build step at runtime; no server-side rendering.

```
Aurora.html
├── styles.css                     ← all visual design tokens & layout
├── image-slot.js                  ← <image-slot> web component (drop-target)
├── tweaks-panel.jsx + babel/react ← live design controls (dev only)
└── Google Fonts: Cormorant Garamond, Instrument Sans, JetBrains Mono
```

Two distribution variants are derived from this source:

| Variant            | File                | Includes Tweaks | Bundled | Use                         |
|--------------------|---------------------|-----------------|---------|-----------------------------|
| Working source     | `Aurora.html`       | yes             | no      | Authoring                   |
| Standalone (full)  | `aurora.html`       | yes             | yes     | Internal review on desktop  |
| Standalone (lean)  | `aurora-mobile.html`| no              | yes     | External review, iOS Safari |

## 2. Design tokens

Defined as CSS custom properties on `:root`; overridden under `[data-mood="…"]`.

| Token            | Snow (default) | Muse        | Stone     | Night     |
|------------------|----------------|-------------|-----------|-----------|
| `--paper`        | `#fbfaf7`      | `#f6ece2`   | `#ecedea` | `#161412` |
| `--paper-deep`   | `#f1eee8`      | `#ecdfd1`   | `#dfe0dc` | `#1f1c19` |
| `--ink`          | `#1a1714`      | `#2a1d16`   | `#181a19` | `#ece6da` |
| `--ink-soft`     | `#3a342e`      | `#4a382e`   | `#353835` | `#c9c3b6` |
| `--ink-muted`    | `#8c8478`      | `#968272`   | `#767a76` | `#807868` |
| `--line`         | `#e2ddd2`      | `#d9c6b3`   | `#cbcdc7` | `#2c2825` |

### Type stack

| Role     | Family                          | Weights         | Use                            |
|----------|--------------------------------|-----------------|--------------------------------|
| Display  | Cormorant Garamond              | 300, 300 italic | Headlines, pull-quotes, signatures |
| Body     | Instrument Sans                 | 400, 500        | Paragraphs, UI                 |
| Mono     | JetBrains Mono                  | 400, 500        | Edition numbers, captions, eyebrows |

### Spacing

- Page gutter: `clamp(20px, 4vw, 56px)` (20px on phone)
- Section padding: `clamp(64px, 11vw, 160px)` (collapsed to 64px on phone)
- Max content width: 1440px

## 3. Layout system

CSS Grid for the page-level skeleton, Flexbox for inline runs. Section breakpoints:

| Breakpoint     | Hero      | Tiers      | Gallery       | Craft     | Story     | Footer    |
|----------------|-----------|------------|---------------|-----------|-----------|-----------|
| ≥901px         | 1.15 / .85| 3-up grid  | 12-col grid   | 2-col     | 2-col     | 4-col     |
| 481–900px      | 1-col     | 1-col      | 6-col grid    | 1-col     | 1-col     | 2-col     |
| ≤480px         | 1-col     | 1-col      | 1-col         | 1-col     | 1-col     | 1-col     |

## 4. Components (detailed design)

### 4.1 Nav (`.nav`)
- Sticky with backdrop blur
- 3-col grid (logo · links · meta+CTA)
- Adds 1px border on scroll > 24px via `.scrolled` class

### 4.2 Hero (`.hero`)
- Edition meta strip with hairline rule
- H1 clamp `(52px, 6.4vw, 96px)` to avoid descender overlap
- Two-column grid; image column holds an `<image-slot>` at 4/5

### 4.3 Tier card (`.tier`)
- Edition number (mono) + edition size (mono) in header
- Image slot (4/5)
- Display heading with italicized second word
- Price-from in mono in the foot

### 4.4 Gallery items (`.g-1`–`.g-5`)
- Staggered top-margins create editorial rhythm at desktop
- Each item: image slot + plate label + italic title

### 4.5 Craft step (`.craft-step`)
- Roman numeral (mono) in 64px gutter
- Display sub-heading + body line at 14.5px

### 4.6 FAQ item (`<details>`)
- Native `<details>`/`<summary>` with custom plus/minus glyph
- Hairline rule above each item

### 4.7 image-slot (web component)
- Drop target with `placeholder` text
- Persists dropped image in `localStorage` keyed by `id`
- Author controls shape & aspect ratio via host CSS

### 4.8 Tweaks panel (dev-only)
- Floating React panel registered via the editor host protocol
- Three controls: palette (radio→select), italic emphasis (radio), marquee toggle
- Values persist into the `EDITMODE-BEGIN…END` JSON block

## 5. Interaction states

| Element       | Default                    | Hover                          | Active / Open               |
|---------------|----------------------------|--------------------------------|-----------------------------|
| Nav link      | `--ink-soft`               | Underline grows L→R, `--ink`   | n/a                         |
| Primary btn   | Filled, ink bg, paper fg   | `translateY(-1px)`             | n/a                         |
| Ghost btn     | Hairline border            | Border darkens to ink          | n/a                         |
| Tier card     | Static                     | Arrow on CTA shifts +4px       | n/a                         |
| FAQ summary   | `+` glyph                  | Cursor pointer                 | `+` collapses to `-`        |

## 6. Detailed design — module specs (Unit-Test inputs)

| Module          | Inputs                                  | Outputs / state                                | Side effects                          |
|-----------------|-----------------------------------------|------------------------------------------------|---------------------------------------|
| `image-slot`    | drop event, attribute `id`               | image src on element                           | writes `localStorage[id]`             |
| Nav scroll bind | `window.scroll` event                    | `.scrolled` class on `#nav`                    | none                                  |
| Newsletter form | submit event                             | clears input, reveals "thanks" caption         | none (mock)                            |
| Tweaks: palette | radio change → `setTweak('mood', v)`     | `data-mood` attr on `<html>`                   | postMessage `__edit_mode_set_keys`    |
| Tweaks: marquee | toggle change                            | `display: none` on `.strip`                    | postMessage                            |
| Tweaks: italics | radio change                             | `font-style` on `h1 em, h2 em`                 | postMessage                            |
