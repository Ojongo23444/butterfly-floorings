# CLAUDE.md — Butterfly Floorings Website & SEO
> Upload this file at the start of every Claude session. It is the single source of truth for this project.
> Always read this file fully before making any changes or suggestions.

---

## 1. Project Overview

| Field | Value |
|---|---|
| **Business** | Butterfly Floorings — Concrete & Epoxy Specialists |
| **Founded** | 2022 |
| **Tagline** | Floors that outlast the moment. |
| **Market** | Greater Toronto Area (GTA), Ontario, Canada |
| **Phone** | 226-829-8485 |
| **Email** | contact@butterflyfloorings.com |
| **Website** | https://www.butterflyfloorings.com |
| **GBP URL** | https://share.google/t0wLO1r8lREVmOrjX |
| **Last Updated** | March 2026 |

**Services offered:** Concrete Polishing, Epoxy Flooring, Concrete Grinding & Surface Preparation, Concrete Floor Leveling, Floor Demolition & Removal.

---

## 2. Technology Stack

| Layer | Tool |
|---|---|
| CMS / Builder | WordPress (local install) + Divi 5 |
| Static Export | Simply Static 3.6.3 — ZIP method — Destination URL: `https://www.butterflyfloorings.com` |
| Version Control | GitHub — public repo: `butterfly-floorings` |
| Hosting / CDN | Cloudflare Pages |
| Contact Form | Web3Forms — Access Key: `0337485c-6c56-43cc-9408-53b46c760864` |
| SSL | Cloudflare SSL/TLS — Full (Strict) |

### Update Workflow (every time)
1. Edit HTML files directly (or via Claude)
2. Push updated files to GitHub repo `butterfly-floorings`
3. Cloudflare Pages auto-deploys within ~60 seconds
4. Verify live site at www.butterflyfloorings.com
5. Submit updated URLs in Google Search Console → URL Inspection → Request Indexing
6. **Always verify Cloudflare Email Obfuscation is OFF after any deploy**

---

## 3. Cloudflare — Critical Settings (must always be correct)

| Setting | Value | Location |
|---|---|---|
| **Email Address Obfuscation** | **OFF** | Scrape Shield |
| **Rocket Loader** | **OFF** | Speed → Optimization |
| **SSL/TLS** | **Full (Strict)** | SSL/TLS |
| **IndexNow** | ON | Search → IndexNow |

> ⚠️ **Email Obfuscation is the #1 recurring issue.** When ON it mangles `contact@butterflyfloorings.com` into `__cf_email__` encoded strings, injects `/cdn-cgi/scripts/5c5dd728/cloudflare-static/email-decode.min.js`, and **truncates the closing JavaScript** — breaking the contact form completely.
>
> **Fix if it happens:** Remove all `__cf_email__` spans, restore `contact@butterflyfloorings.com`, remove the `/cdn-cgi/scripts/` tag, restore the closing `IntersectionObserver` + nav scroll JS + `</script></body></html>`.

---

## 4. Design System

### Colours
| Variable | Hex | Usage |
|---|---|---|
| `--bg` | `#0e0f11` | Main page background |
| `--bg-card` | `#1e2028` | Service cards, form background |
| `--blue` | `#1e90ff` | CTAs, accents, highlights |
| `--text` | `#e8eaed` | Primary body text |
| `--muted` | `#6b7280` | Secondary / descriptive text |

### Typography
- **Headings:** Barlow Condensed (Google Fonts) — weights 400, 600, 700, 800
- **Body:** Inter (Google Fonts) — weights 300, 400, 500, 600
- **Style:** Dark industrial theme — blueprint grid lines, blue glow effects, noise texture, scroll fade-up animations

### Logo Specs
- Header logo: `butterfly-floorings-logo-no-tagline.svg`
- Footer logo: `butterfly-floorings-logo-tagline.svg`
- Site icon: `butterfly-floorings-icon-512.png`
- `textLength="148" lengthAdjust="spacingAndGlyphs"` on both BUTTERFLY and FLOORINGS text
- Blue separator line: `#1e90ff` opacity 0.35 — Font weight: Barlow Condensed 600

---

## 5. Page Inventory (current — March 2026)

| File | URL | Target Keyword | Vol/mo | Status |
|---|---|---|---|---|
| `index.html` | `/` | Brand / general | — | Live |
| `epoxy-flooring-toronto.html` | `/epoxy-flooring-toronto.html` | epoxy flooring Toronto | 800–1,200 | Live |
| `epoxy-flooring-mississauga.html` | `/epoxy-flooring-mississauga.html` | epoxy flooring Mississauga | 150–300 | Live |
| `garage-floor-epoxy-gta.html` | `/garage-floor-epoxy-gta.html` | garage floor epoxy coating GTA | 200–400 | Live — NEW |
| `concrete-floor-grinding-toronto.html` | `/concrete-floor-grinding-toronto.html` | concrete floor grinding Toronto | 100–200 | Live — NEW |
| `floor-leveling-toronto.html` | `/floor-leveling-toronto.html` | floor leveling contractor Toronto | 100–200 | Live — NEW |
| `concrete-polishing-toronto.html` | `/concrete-polishing-toronto.html` | concrete polishing Toronto | 400–700 | Live |
| `gallery.html` | `/gallery.html` | — | — | Live |

### Files to Keep in GitHub (never delete)
`index.html`, `epoxy-flooring-toronto.html`, `epoxy-flooring-mississauga.html`, `garage-floor-epoxy-gta.html`, `concrete-floor-grinding-toronto.html`, `floor-leveling-toronto.html`, `concrete-polishing-toronto.html`, `gallery.html`, `sitemap.xml`, `robots.txt`, `CNAME` (critical — do not delete), `/images/` folder

---

## 6. Contact Form

- **Handler:** Web3Forms via `fetch()` to `https://api.web3forms.com/submit`
- **Access Key:** `0337485c-6c56-43cc-9408-53b46c760864`
- **Field IDs:** `#first_name`, `#last_name`, `#phone`, `#email`, `#service`, `#message`
- **Submit button:** `<button type="button" class="form-submit">` — must have `type="button"`
- **Do NOT include** `formData.append('redirect', 'false')` — Web3Forms treats this as a redirect URL and rejects the submission
- The contact form **only exists on `index.html`** — all service pages link to `index.html#contact`

### If the form stops working, check in this order:
1. Cloudflare Email Obfuscation is OFF (most common cause)
2. `type="button"` is on the submit button
3. No `redirect: 'false'` field in the formData
4. Web3Forms access key is verified and active at web3forms.com
5. Closing `</script></body></html>` tags are present at end of index.html

---

## 7. Known Issues & Watch Points

### "Ready to Start?" Button — FIXED (March 2026)
`.service-card::after` pseudo-element had no `pointer-events: none`, so it sat above the CTA button and blocked clicks. Fixed by adding `pointer-events: none` to `.service-card::after` in index.html CSS.

### Cloudflare Email Obfuscation — Recurring
Has broken the site multiple times. See Section 3. Always verify OFF after any Cloudflare settings change.

### Gallery Page — Image Files
`gallery.html` references images in `/images/` folder. These must be uploaded to GitHub for images to display. Current filenames: `epoxy-flake-garage-floor-mississauga.jpg`, `residential-epoxy-flooring-brampton.jpg`, `warehouse-concrete-polishing-toronto.jpg`, `industrial-concrete-polishing-gta.jpg`, `epoxy-garage-floor-mississauga.jpg`, `epoxy-flooring-butterfly-floorings.jpg`, `og-image.jpg` (root level).

---

## 8. SEO Status

### Completed
- Meta descriptions, canonical tags, OG/Twitter tags — all pages
- robots meta `index, follow` — all pages
- Geo tags `CA-ON` — all pages
- LocalBusiness JSON-LD schema on homepage — includes services, reviews, areaServed, sameAs (GBP URL)
- AggregateRating 5 stars, 3 reviews (Matthew, Bassey, Femi)
- FAQ sections on all service pages
- Keyword-rich image filenames and alt text
- sitemap.xml — 8 pages
- robots.txt — allows all, references sitemap
- Google Maps embed in contact section (index.html)
- Internal linking — all pages cross-link with keyword-rich anchor text
- New pages: garage epoxy, concrete grinding, floor leveling

### Pending (do not mark done until confirmed)
- Google Search Console setup + sitemap submission
- Bing Webmaster Tools — submit sitemap at bing.com/webmasters
- sameAs — add HomeStars, Houzz, Yelp URLs once profiles created
- Google reviews — need 10+ on GBP for Maps Pack visibility
- Real project photos uploaded to /images/ folder in GitHub

---

## 9. To-Do List (next session priority order)

### 🔴 Immediate
| # | Item | Details | Files |
|---|---|---|---|
| 1 | **Fix H1 / H2 swap** | H1 is styled as invisible eyebrow. Hero text "Surface Precision. Perfected." is H2 with zero keywords. Swap them — H1 should be the prominent visible heading. | `index.html` |
| 2 | **Fix hero image alt text** | Hero image is `epoxy-garage-floor-mississauga.jpg` but alt says "Polished concrete warehouse floor." Fix to match the actual image. | `index.html` |
| 3 | **Add address/hours to schema** | Add `streetAddress`, `postalCode`, and `openingHours` to LocalBusiness JSON-LD. Even a postal code helps Google Maps trust signal. | `index.html` |

### 🔵 New Pages
| # | Keyword | URL | Vol/mo | Competition |
|---|---|---|---|---|
| 4 | commercial epoxy flooring Ontario | `/commercial-epoxy-flooring-ontario.html` | 150–300 | Medium |
| 5 | floor demolition removal Toronto | `/floor-demolition-removal-toronto.html` | Low | Low |

### ⚪ Ongoing
| # | Item |
|---|---|
| 6 | Add HomeStars, Houzz, Yelp URLs to `sameAs` in schema once profiles created |
| 7 | Collect Google reviews — text every completed client. Need 10+ for Maps Pack. |
| 8 | Set up Google Search Console, submit sitemap, request indexing after every deploy |
| 9 | Submit to local directories: HomeStars, Houzz, Yelp Canada, Yellow Pages Canada, BBB. Identical NAP on every platform. |
| 10 | Upload real project photos to `/images/` folder in GitHub |

---

## 10. Keyword Priority Reference

| Keyword | Vol/mo | Difficulty | Page | Timeline |
|---|---|---|---|---|
| epoxy flooring near me | 1,500–3,000 | High | GBP only | 4–8 wks after 10+ reviews |
| epoxy flooring Toronto | 800–1,200 | Medium | ✅ live | 3–6 months |
| concrete polishing Toronto | 400–700 | Medium | ✅ live | 2–4 months |
| garage floor epoxy coating GTA | 200–400 | Low | ✅ live | 4–8 weeks |
| epoxy floor coating GTA | 200–400 | Low | No page | 4–8 wks after page built |
| commercial epoxy flooring Ontario | 150–300 | Medium | No page | 4–7 months |
| epoxy flooring Mississauga | 150–300 | Low | ✅ live | Ranking now |
| concrete floor grinding Toronto | 100–200 | Low | ✅ live | 4–8 weeks |
| floor leveling contractor Toronto | 100–200 | Low | ✅ live | 4–8 weeks |

---

## 11. Ranking Timeline Expectations

| Milestone | Estimated Timeline |
|---|---|
| Google Maps Pack visibility | 4–8 weeks after GBP has 10+ reviews |
| Long-tail local keywords Page 1 | 2–4 months |
| Mid-competition city keywords | 4–7 months |
| "Epoxy flooring Toronto" Page 1 | 6–12 months |

---

## 12. How to Start a New Claude Session

1. Say: *"I am continuing work on the Butterfly Floorings website."*
2. Upload this `CLAUDE.md` file
3. Upload the latest HTML files from GitHub that you want to change
4. Tell Claude which to-do items to work on
5. After receiving updated files, push to GitHub
6. Verify live site at www.butterflyfloorings.com
7. **Verify Cloudflare Email Obfuscation is OFF**
8. Submit changed URLs in Google Search Console → URL Inspection → Request Indexing
9. Update this `CLAUDE.md` with any new completed items or decisions made
