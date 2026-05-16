# 01 — High-Level Flow

## Concept of Operations

Aurora is a single-page marketing & catalog site for a small, high-end handcrafted art doll atelier. The site exists to do four things, in this order of importance:

1. **Establish trust and tone** — a quiet, premium aesthetic that signals craft and intentionality.
2. **Communicate the three product tiers** — Originals (1/1), Limited Editions (numbered run), Studio Line (time-limited).
3. **Capture interest** — waitlist signups, newsletter subscriptions.
4. **Educate** — process, materials, brand story, frequently asked questions.

It is not (in v1) a checkout, an account system, or a CMS. Purchases happen by direct correspondence with the atelier.

## Primary user journey

```
  Discover ──► Land on hero ──► Skim three tiers ──► Browse gallery
                                                          │
                                                          ▼
                                              Read process / story
                                                          │
                                                          ▼
                                                Reach FAQ / CTA
                                                          │
                                                          ▼
                                          Join waitlist OR subscribe
```

Typical first session lasts 90–180 seconds. The hero, marquee strip, and tier overview must communicate the brand within the first ~10 seconds.

## Personas

| Persona              | Goal                                         | Entry          | Exit / conversion          |
|----------------------|----------------------------------------------|----------------|----------------------------|
| Collector (returning)| See latest release, join waitlist            | Hero → Tiers   | Waitlist                   |
| Collector (new)      | Evaluate trust, understand tiers & price     | Hero → Story   | Newsletter                 |
| Curator / press      | Understand brand & process, get materials    | Hero → Craft   | Newsletter / Press contact |
| Casual visitor       | Curiosity, may share                         | Hero → Gallery | (passive)                  |

## Page anatomy (in scroll order)

1. **Navigation** — sticky, brand mark, anchors, edition caption, waitlist CTA.
2. **Hero** — feature headline, lede, dual CTAs, feature image, edition meta.
3. **Marquee strip** — atelier credentials, slow horizontal scroll.
4. **Collections** — three tiers in a single bordered grid.
5. **Gallery** — five editorial plates in an asymmetric grid.
6. **Craft** — five-step process on a tinted block with a sticky media column.
7. **Story** — brand narrative with founder signature.
8. **Testimonials** — three pull-quotes in a bordered grid.
9. **CTA banner** — release announcement on inverted ink-block.
10. **FAQ** — six expandable items.
11. **Newsletter** — quiet inline form.
12. **Wordmark** — large italic finale.
13. **Footer** — four columns + base caption.

## Out of scope (v1)

- Account creation, sign-in
- Cart and checkout
- Localization beyond English
- Per-piece detail pages
- Editorial CMS

## Future phases

- v2: per-piece detail pages, edition counters
- v3: collector account & wishlist
- v4: limited online checkout for Studio Line only
