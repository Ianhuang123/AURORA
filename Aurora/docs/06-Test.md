# 06 — Test Execution & Results

Run: 2026-05-15 · Build: `Aurora.html` @ v1 (Snow palette default) · Bundles: `aurora.html` (1.7 MB), `aurora-mobile.html` (557 KB).

Legend: ✅ pass · ⚠️ pass with note · ❌ fail · ⏳ not run

## §U — Unit

| TC     | Result | Notes                                                                     |
|--------|--------|---------------------------------------------------------------------------|
| TC-001 | ✅      | `image-slot` persisted hero JPG; reload survived                          |
| TC-002 | ⚠️      | Slot without id renders in-session only — currently every slot has an id  |
| TC-003 | ✅      | `.scrolled` class observed; hairline border appears                       |
| TC-004 | ✅      | Confirmation caption revealed; input cleared                              |
| TC-005 | ✅      | Browser blocks submit with native validation message                      |
| TC-006 | ✅      | `<html data-mood="muse">` reflected; tokens repainted                     |
| TC-007 | ✅      | `h1 em, h2 em` rendered upright after toggle                              |
| TC-008 | ✅      | `.strip` hidden                                                           |
| TC-009 | ✅      | `+` toggled to `-`; content reflows                                       |

## §I — Integration

| TC     | Result | Notes                                                                     |
|--------|--------|---------------------------------------------------------------------------|
| TC-010 | ✅      | All 13 sections render in order at 1440×900                               |
| TC-011 | ✅      | Palette flip warm → night repaints all dependent tokens; CTA inverts      |
| TC-012 | ✅      | Anchors scroll with `scroll-margin-top: 80px` clearing the sticky nav     |
| TC-013 | ✅      | Edition labels: "1 of 1", "Edition of 24", "Time-limited window"          |
| TC-014 | ✅      | 0 console errors on first paint (last `done` confirmed)                   |

## §S — System

| TC     | Result | Notes                                                                     |
|--------|--------|---------------------------------------------------------------------------|
| TC-015 | ✅      | No horizontal scroll at 360, 414, 768, 1024, 1440, 2560                   |
| TC-016 | ✅      | Smallest computed body text on phone: 14px (mono caption 11.5 → 11px floor still readable; acceptable per N-004 because mono is for captions, not body) |
| TC-017 | ✅      | Hero h1 clamp capped at 96px after verifier feedback; no descender overlap with `.hero-lede` |
| TC-018 | ⚠️      | Spot-checked: body 4.8:1, mono captions 4.5:1, ghost-btn 4.6:1 — at edge of AA for muted ink; future tightening recommended |
| TC-019 | ✅      | `aurora-mobile.html` = 557 KB total; full bundle 1.7 MB (within budget)   |
| TC-020 | ✅      | Opened lean bundle offline; Cormorant falls back to Georgia gracefully    |
| TC-021 | ✅      | Lean bundle renders on iOS Safari 17 from Files app (issue resolved by stripping Babel) |

## §A — Acceptance

| TC     | Result | Notes                                                                     |
|--------|--------|---------------------------------------------------------------------------|
| TC-022 | ✅      | Returning-collector path: hero → "Join the waitlist" CTA in 2 clicks      |
| TC-023 | ✅      | Press path: hero → §III Process → §VII Letter in 3 anchors                |
| TC-024 | ✅      | No exclamation marks in copy; no superlatives ("best", "ultimate", etc)   |
| TC-025 | ✅      | All slots accept photography; placeholders carry photographic prompts     |
| TC-026 | ⏳      | Awaiting atelier stakeholder sign-off                                     |

## Defects opened

| ID    | Severity | Origin   | Description                                                            | Status   |
|-------|----------|----------|------------------------------------------------------------------------|----------|
| D-001 | High     | TC-017 (pre-fix) | Hero h1 at 132px wrapped to 4 lines and overlapped `.hero-lede` | Closed — clamp lowered to 96px, column ratio widened to 1.15/.85 |
| D-002 | High     | TC-021 (pre-fix) | iOS Safari opening downloaded `aurora.html` stuck on splash    | Closed — produced `aurora-mobile.html` without Babel/React       |
| D-003 | Med      | TC-018           | Mono captions sit at WCAG AA floor; future palette tweaks should not weaken | Open  |

## Summary

- **24/26 cases pass** (1 awaiting sign-off, 1 pass-with-note on contrast floor).
- **2 defects closed** during build (hero overlap, iOS splash-stuck).
- **1 defect open**: contrast watchlist for mono captions.
- **Recommend**: proceed to v1 ship; queue D-003 mitigation for next iteration.
