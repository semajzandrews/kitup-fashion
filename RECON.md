# Kitup Fashion — Recon & Art Direction

## Verified facts (the only facts used in copy)
- **Name:** Kitup Fashion
- **Category:** Clothing / streetwear boutique
- **Address:** 195 Main St, City of Orange, NJ 07050
- **Phone:** (973) 855-7431  (`tel:+19738557431`)
- **Rating:** 5.0 stars, 9 Google reviews
- **Hours (12-hour, America/New_York):**
  - Mon to Thu: 10 AM to 8 PM
  - Fri & Sat: 10 AM to 10 PM
  - Sunday: Closed
- **Map:** keyless Google embed (Ramos pattern) centered on the address string
  `https://www.google.com/maps?q=195+Main+St,+City+of+Orange,+NJ+07050&z=16&output=embed`

No social handle is shown. None was verifiable as exactly this business, so per the
verified-socials rule it is omitted.

## Art direction
- **Concept:** Bold editorial streetwear. Lookbook energy, "fit check" tone, confident and
  fashion-forward without being loud for its own sake.
- **Palette:** high-contrast black (`#0a0a0a`) + warm paper (`#f4f3ee`) + ONE electric accent,
  acid green (`#c6ff00`). The accent carries the brand mark, key words, CTAs, the status pill,
  and the review moment.
- **Type pairing (Fontshare):**
  - Display: **Clash Display** (brutalist oversized grotesk) for headlines, with an
    outlined/`-webkit-text-stroke` treatment on "DIFFERENT".
  - Sub-display / labels: **Khand** (condensed tactical grotesk) for nav links, kickers,
    pills, marquee.
  - Body: **Satoshi** (clean neutral grotesk).
  This trio is not reused by any sibling in the sprint.

## Signature interaction (assigned)
**Pinned editorial scroll** — a sticky image column (the "stage") holds one fixed lookbook
shot while the captions/looks scroll past on the other side. As each caption reaches viewport
center, the pinned image, the `01/04` counter, and the big stage label cross-fade to match.
Fully VERTICAL, no horizontal carousel.

Implementation note / hard lesson logged: the first cut used an IntersectionObserver with a
narrow `-44%/-44%` rootMargin band. That band could never reach the FIRST or LAST caption
(not enough scroll runway before/after them against the sticky pin), so looks 1 and 4 got
stuck. Replaced with a scroll-driven "closest caption midpoint to viewport center" picker on a
passive scroll listener. Verified all four looks (0→1→2→3) activate in sequence, including the
first and last.

**Mobile fallback (≤760px):** the sticky pin is dropped entirely (`display:none`) and each
look renders its own inline 4:5 image above the caption — a clean stacked lookbook. Verified at
375px: no horizontal overflow (document scrollWidth = 375), nav collapses to a 46×46px acid
call icon (right edge 360px, inside the viewport), nav links hidden, collections grid → 2-up,
lookbook → single column.

## Imagery (all Unsplash, each used once, zero reuse across the sprint)
Siblings in this sprint all source from Pexels; this build uses Unsplash exclusively to
guarantee no shared photo. Every shot was eyeballed to confirm it reads as streetwear/apparel.

- Hero: `photo-1523398002811` — black/yellow windbreaker against street posters (urban streetwear)
- Lookbook 01 "Bold & loud": `photo-1529139574466` — red graphic sweatshirt + black overshirt, blue sky
- Lookbook 02 "Everyday uniform": `photo-1571945153237` — white tee + beanie, easy staple
- Lookbook 03 "Laced up": `photo-1556906781` — black/orange high-tops, city skyline
- Lookbook 04 "After dark": `photo-1509631179647` — neon editorial pose, going-out fit
- Collection Layers: `photo-1551232864` — rolling rack of jackets/outerwear
- Collection Tees: `photo-1521572163474` — crisp white tee on model
- Collection Fleece: `photo-1604176354204` — folded crewneck flat-lay
- Collection Denim: `photo-1542272604` — stacked jeans, washes
- Collection Footwear: `photo-1542219550` — grey/gold high-tops on dark

## Copy notes
- Lead line "Fits that hit different" with the neighborhood placement ("the spot on Main
  Street"). Specific, human, no generic welcome copy.
- No em dashes anywhere in visible copy (periods / "and" / commas only). The bysemaj credit
  uses a period, not a dash.
- Live "Open now / Closed" pill computed from the real hours in America/New_York, 12-hour
  output throughout. Logic verified across open, before-open, after-close, and Sunday-closed
  cases (e.g. Sun → "Closed · opens tomorrow 10 AM", Sat 10 PM → "Closed · opens Mon 10 AM").

## Build rule compliance
- Real per-brand nav bar with brand mark + section links + persistent call CTA; mobile collapses
  to a 46px call icon (number kept in `aria-label`). ✓
- Footer carries name, real address, real phone, hours, a persistent call CTA, and a tasteful
  "built by bysemaj.com" credit linking https://bysemaj.com, styled to this brand. ✓
- 12-hour time everywhere; live open/closed pill. ✓
- No em dashes in visible copy. ✓
- No image reused; every photo reads as the category. ✓
- Keyless Google Maps embed on the real address (Ramos pattern); iframe src verified. ✓
- Mobile-first, audited at 375px, no overflow; smooth in-page anchor scroll. ✓
- Accessibility: semantic landmarks (`header`/`main`/`section`/`footer`), real alt text on all
  content images, decorative SVGs `aria-hidden`, icon-only call button has `aria-label`,
  visible focus ring (acid outline), AA-contrast text on dark and on acid surfaces.

## Verification (preview at 375px and 1280px)
- No console errors.
- Hero renders (desktop + mobile screenshots confirmed).
- Signature pinned scroll: all 4 looks + shots + counter + label sync correctly on scroll.
- Review section: acid bg, ink text, "5.0 ★★★★★ · 9 reviews", rotating quotes.
- Map iframe: correct keyless Google embed src + descriptive title.
- Footer credit links to bysemaj.com.
- Status pill live: "Open now · until 8 PM" at build time (Wed ~6:53 PM ET).

Note: the headless preview screenshot tool rendered the dark sections and any
programmatically-scrolled frame as blank (it captures the top-of-page frame and does not honor
JS `scrollTo`/dark-section rasterization). The hero (at scroll 0) screenshots correctly; all
other sections were verified via DOM geometry + computed styles, which matched the design. In a
real browser the sticky pin and dark sections render normally — re-verify the map and scroll in
a real Chrome before going LIVE.
