# 02 — Requirements

Each requirement carries a stable ID (`R-NNN`). Implementations and test cases trace back to these.

## Functional requirements

| ID    | Requirement                                                                                  | Priority |
|-------|----------------------------------------------------------------------------------------------|----------|
| R-001 | The site shall present a hero section with brand headline, lede, and two CTAs.               | Must     |
| R-002 | The navigation shall be sticky and contain links to each major section.                      | Must     |
| R-003 | The site shall display three product tiers (Originals, Limited Editions, Studio Line) in a single bordered grid, each with edition info, description, price-from, and a CTA. | Must |
| R-004 | The site shall provide an editorial gallery of at least five image slots in an asymmetric grid. | Must  |
| R-005 | The site shall present a five-step craftsmanship process on a contrasting background.        | Must     |
| R-006 | The site shall present a brand-story section with a portrait image and founder signature.    | Must     |
| R-007 | The site shall display three collector testimonials in a bordered three-column grid.         | Must     |
| R-008 | The site shall include a CTA banner announcing the next release.                             | Must     |
| R-009 | The site shall provide a FAQ with at least six expandable items.                             | Must     |
| R-010 | The site shall offer a newsletter signup with email input and inline confirmation.           | Must     |
| R-011 | The footer shall present brand mark, three link columns, and base caption.                   | Must     |
| R-012 | Image placeholders shall accept drag-and-drop image uploads and persist them per slot.       | Must     |
| R-013 | The user shall be able to switch between at least three color moods (Snow, Muse, Stone, Night). | Should |
| R-014 | The user shall be able to toggle italic emphasis on display headings.                        | Should   |
| R-015 | The user shall be able to hide the marquee strip.                                            | Could    |
| R-016 | A standalone offline version of the page shall be exportable.                                | Should   |

## Non-functional requirements

| ID    | Requirement                                                                                  | Target           |
|-------|----------------------------------------------------------------------------------------------|------------------|
| N-001 | The page shall render correctly across viewports from 360px to 2560px.                       | Pass             |
| N-002 | The mobile breakpoint (≤900px) shall collapse all multi-column layouts to single column.     | Pass             |
| N-003 | The page shall produce no console errors on first paint.                                     | 0 errors         |
| N-004 | Body copy size shall not fall below 14px at any viewport.                                    | ≥14px            |
| N-005 | Display headings shall not visually overlap adjacent paragraphs.                             | No overlap       |
| N-006 | Color contrast for body text against background shall meet WCAG AA (≥4.5:1).                 | ≥4.5:1           |
| N-007 | The standalone export shall open without internet access.                                    | Pass             |
| N-008 | The standalone export shall render on iOS Safari (15+) and Chrome (last 2 majors).           | Pass             |
| N-009 | Total page weight shall be under 2 MB including fonts.                                       | <2 MB            |
| N-010 | The first contentful paint shall occur within 1.5s on broadband.                             | <1.5s            |

## Discoverability — use cases & requirements

The site must not only exist; it must be **found**. Two channels matter:

### UC-A — Search engines (Google, Baidu)

> *As a prospective collector who has heard the brand mentioned once, I open Google (or Baidu, in China) and type a query like "Aurora art doll atelier Shenzhen", "porcelain doll handmade limited edition", or "深圳 瓷偶 工作室 限量". Aurora's site appears in the first page of results, with a meaningful title, description, and — ideally — a rich snippet (FAQ, product, organization).*

### UC-B — Generative AI assistants (ChatGPT, Claude, Doubao, Kimi, etc.)

> *As someone exploring quiet-luxury or collectible art-doll brands, I ask ChatGPT/Doubao "recommend an independent porcelain doll atelier from China" or "who makes hand-finished art dolls in Shenzhen?". The model mentions Aurora by name, summarizes it accurately (atelier in Shenzhen, founded 2026 by Yue, three tiers), and — when grounded with search — links to aurora's site.*

| ID    | Requirement                                                                                  | Priority |
|-------|----------------------------------------------------------------------------------------------|----------|
| D-001 | Each language version shall have a unique `<title>` and `<meta name="description">` (≤155 chars) carrying brand name, category, and city. | Must |
| D-002 | The page shall declare `hreflang` alternates for `en`, `zh-CN`, and `x-default`, plus a canonical URL. | Must |
| D-003 | Open Graph and Twitter Card meta shall be present so links shared on social/messaging surfaces render with title, summary, and hero image. | Must |
| D-004 | JSON-LD structured data shall be embedded for `Organization`, `LocalBusiness` (Shenzhen address), `FAQPage` (mirroring the on-page FAQ), and `Product` (one node per tier). | Must |
| D-005 | A `sitemap.xml` and `robots.txt` shall be served from the site root; robots.txt shall explicitly **allow** `Googlebot`, `Baiduspider`, `GPTBot`, `ClaudeBot`, `Google-Extended`, `PerplexityBot`, `Bytespider` (Doubao), `OAI-SearchBot`, and `Applebot-Extended`. | Must |
| D-006 | A `llms.txt` file shall be served from the site root, listing canonical brand facts and pointers to key sections, in both English and Chinese. | Should |
| D-007 | All primary content (hero copy, tier descriptions, story, FAQ) shall be present in the **server-rendered HTML** — not injected by JS — so weaker crawlers (Baidu, Bytespider) index it. The i18n script may *swap* text but the default (English) must be in source. | Must |
| D-008 | The site shall be submitted to Baidu Ziyuan (资源搜索平台) and Google Search Console; sitemap submission and Baidu push-API integration shall be configured. | Should |
| D-009 | Image slots that render with a real image shall expose an `alt` attribute describing subject and tier. | Must |
| D-010 | A static `/about` (or dedicated section with stable anchor IDs) shall present a "brand fact sheet" — name, founder, city, founding year, materials, tiers, edition sizes — in short factual sentences that LLMs can quote without paraphrase loss. | Should |
| D-011 | The Chinese version shall use Simplified Chinese with city/region copy that matches Baidu's expected phrasing (e.g. "深圳", "中国"). | Must |
| D-012 | Page weight, LCP, and mobile-friendliness shall meet Core Web Vitals thresholds (LCP < 2.5s, CLS < 0.1) — both Google and Baidu rank on speed. | Must |
| D-013 | External signals: the brand shall maintain at least one entry on a Chinese platform indexed by Baidu/Doubao (e.g. 小红书, 微信公众号, 百度百科) and one English platform (e.g. press feature, directory listing). | Should |

## Brand & content requirements

| ID    | Requirement                                                                                  |
|-------|----------------------------------------------------------------------------------------------|
| B-001 | Tone shall be quiet, poetic, restrained — no exclamation marks, no aggressive sales copy.    |
| B-002 | Type system shall pair a refined serif (display) with a neutral sans (body) and a mono accent (captions). |
| B-003 | Color palette shall use soft neutrals — paper whites, stone greys, warm earth ink — no saturated accent. |
| B-004 | Edition numbers, dates, and atelier credentials shall be rendered in monospace.              |
| B-005 | Imagery shall be photographic; no illustrated or generated decorative art.                   |
