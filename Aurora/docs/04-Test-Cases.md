# 04 — Test Cases

Each case carries a unique `TC-NNN`, the requirement(s) it verifies (`R-NNN` / `N-NNN`), the V-Model level (U = unit, I = integration, S = system, A = acceptance), and a pass criterion.

## Unit (U)

| TC     | Level | Covers   | Description                                                       | Pass criterion                                              |
|--------|-------|----------|-------------------------------------------------------------------|-------------------------------------------------------------|
| TC-001 | U     | R-012    | Drop a JPG on `image-slot#hero`; reload                           | Image visible after reload                                  |
| TC-002 | U     | R-012    | Drop on slot without `id`                                         | Image visible in session, not persisted (warning OK)        |
| TC-003 | U     | R-002    | Scroll past 24px                                                  | `#nav` gains `.scrolled` class with hairline border         |
| TC-004 | U     | R-010    | Submit newsletter with valid email                                | Input clears, "Thank you" caption appears                   |
| TC-005 | U     | R-010    | Submit newsletter with invalid email                              | Native validation blocks submit                             |
| TC-006 | U     | R-013    | Tweaks → Palette = "Muse"                                         | `<html data-mood="muse">`, background turns cream           |
| TC-007 | U     | R-014    | Tweaks → Italics = "none"                                         | `h1 em, h2 em` render upright in `--ink`                    |
| TC-008 | U     | R-015    | Tweaks → Marquee = off                                            | `.strip` becomes `display: none`                            |
| TC-009 | U     | R-009    | Open and close a FAQ `<details>`                                  | `+` toggles to `-`; body height animates open               |

## Integration (I)

| TC     | Level | Covers          | Description                                                | Pass criterion                                       |
|--------|-------|-----------------|------------------------------------------------------------|------------------------------------------------------|
| TC-010 | I     | R-001..R-011    | Full scroll from hero → footer at 1440×900                 | All 13 sections render in order; no overlap         |
| TC-011 | I     | R-013, B-003    | Switch palette warm → night                                | All `--ink*` and `--paper*` tokens flip; CTA inverts |
| TC-012 | I     | R-002           | Click each nav anchor                                      | Page scrolls to matching `#id` with offset for sticky nav |
| TC-013 | I     | R-003, B-002    | All three tiers render                                     | Distinct edition labels: "1 of 1", "Edition of 24", "Time-limited window" |
| TC-014 | I     | N-003           | First load, no user interaction                            | 0 console errors                                     |

## System (S)

| TC     | Level | Covers          | Description                                                | Pass criterion                                       |
|--------|-------|-----------------|------------------------------------------------------------|------------------------------------------------------|
| TC-015 | S     | N-001, N-002    | Render at 360, 414, 768, 1024, 1440, 2560                  | No horizontal scroll; gallery collapses correctly    |
| TC-016 | S     | N-004           | Inspect smallest body text on phone                        | Computed `font-size` ≥ 14px                          |
| TC-017 | S     | N-005           | Inspect hero h1 against `.hero-lede`                       | Bounding rects do not overlap                        |
| TC-018 | S     | N-006           | Run contrast check on body, mono caption, ghost-btn text   | All ≥ 4.5:1                                          |
| TC-019 | S     | N-009           | Measure total transferred bytes                            | < 2 MB                                               |
| TC-020 | S     | R-016, N-007    | Open `aurora-mobile.html` with no network                  | Renders fully; fonts substitute gracefully           |
| TC-021 | S     | N-008           | Open `aurora-mobile.html` on iOS Safari 17                 | All sections render; no infinite splash              |

## Acceptance (A)

| TC     | Level | Covers          | Description                                                | Pass criterion                                       |
|--------|-------|-----------------|------------------------------------------------------------|------------------------------------------------------|
| TC-022 | A     | flow §journey   | Returning collector path: hero → tiers → waitlist          | ≤4 clicks, ≤30s walkthrough                          |
| TC-023 | A     | flow §journey   | Press path: hero → craft → newsletter                      | All info findable without site search                |
| TC-024 | A     | B-001           | Read all body copy aloud                                   | No exclamation marks; no sales superlatives          |
| TC-025 | A     | B-005           | Audit all decorative imagery                               | All slots accept photography only; no illustrated decor |
| TC-026 | A     | overall         | Stakeholder review                                         | Signed off by design + atelier                       |
