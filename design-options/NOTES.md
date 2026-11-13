# Homepage design options - Dr. Shruti Grover

Prepared 13 November 2026 for Mayank, to pick one direction for the clinic homepage.

- `index.html` - chooser page with the four options, in the order 2, 3, 5, 6.
- `2/index.html`, `3/index.html`, `5/index.html`, `6/index.html` - the four homepages. Each one is a single
  self-contained file: inline CSS, Google Fonts, no framework, no build step, relative links only.
- `shots/` - full-page screenshots at 1440px and 390px, `opt*-390-top.png` (first phone screen, with the sticky
  bar in place), `opt*-1440-mid.png` and `opt*-390-mid.png` (mid-scroll, so the sticky and scroll-driven states are
  visible) and `opt*-preview.jpg` (the card image on the chooser page).
- `../../scripts/tools/cdp.js` and `../../scripts/tools/shots.sh` - the small Chrome driver used to take the shots
  and to measure the pages. No npm install needed.

Options 1 (Clinical calm) and 4 (Doctor-first authority) were **deleted on 13 November 2026**: Mayank's feedback was
"These don't look like modern options at all." They are replaced by two motion-led options, 5 (Flow) and 6 (Pulse).

All four pages carry the same facts, in the same order: header, hero, her story (MS), conditions treated, how a
first visit works, credentials, location, FAQ (4), booking (WhatsApp + form), footer, sticky "Book on WhatsApp" bar
on mobile.

**What the review round changed (13 November 2026).** The reviewer's ten findings are listed at the end of this file,
under **Review notes**. The big ones: option 5's sticky story now really sticks (it was taller than the space it had
to stick in, so the browser dropped the offset); option 6's headline no longer reads as a treatment claim; every page
now carries the NMC AI source mark, worded as *pending review* because Dr. Grover has not read the copy yet; the
390px full-page shots were retaken without the fixed WhatsApp bar, which had been painted in the middle of the page;
the location strings are now driven by one `CLINIC` object instead of being copied around; and LCP and CLS are now
measured with Lighthouse instead of guessed.

## How to review

1. Open `index.html` in a browser (or serve the folder: `python3 -m http.server`).
2. Open each option on a phone (390px) and a laptop (1440px). The screenshots in `shots/` are the same thing.
3. Pick one, or say "option 2 but with option 5's motion". Mixed directions are normal and cheap to do.
4. Note anything that reads wrong for a family in Delhi/NCR: language, tone, how much is on the page.

---

## 1. Research: what makes modern health and startup sites feel premium

Every site below was **read on 13 November 2026** (the page source was fetched and read, not remembered). The counts in
the last column are literal matches in the page source on that date, which is how the motion stack of each site was
identified.

| Site | URL | What it does | Motion stack seen in the page source |
|---|---|---|---|
| Function Health | https://www.functionhealth.com/ | The clearest example of the modern premium-health look: a plain promise in the H1 ("Check your health."), numbered steps 01/02/03, a card grid (Action Plan, Clinician Notes, Private AI Chat), animated stat counters, and a looping marquee of condition names with an explicit "Pause motion / Play motion" control. | time-based CSS/JS transitions, marquee, counters, media queries for reduced motion |
| Superpower | https://superpower.com/ | Full-height video panels, a fast pitch, sticky panels. The most polished of the set, and the heaviest. | GSAP (29 mentions), Lenis smooth scroll (13), Swiper (7), ScrollTrigger (2), `prefers-reduced-motion` handled 13 times, `backdrop-filter` 50 times, `transform: translate` 35 times |
| Oura | https://www.ouraring.com/ | Big calm type over a slow product film, then a scroll of clean feature blocks. | `.mp4`/`.webm` hero media, 51 inline SVG `viewBox` graphics, 4 `will-change` |
| Parsley Health | https://www.parsleyhealth.com/ | Quiet, high-trust membership page: one clear offer, no shouting, everything inline SVG so it stays sharp. | 74 inline SVG `viewBox` graphics, 1 `will-change` (almost no JS-driven motion) |
| Headspace | https://www.headspace.com/ | Friendly illustration-led storytelling with characters that move. | Lottie vector animation (12 mentions), 8 marquee references, 126 inline SVGs |
| Linear | https://linear.app/ | The reference for dark, precise, product-led motion: layers slide, panels track the cursor, gradients move behind glass. | 14 marquee references, 571 inline SVGs, 13 `clip-path` (gradient-masked edges) |
| Stripe | https://stripe.com/ | Cinematic gradients and section transitions that feel like film, with everything else kept still. | 149 inline SVGs, 62 `clip-path` gradient masks, 2 marquee |
| Vercel | https://vercel.com/ | Sharp dark grid, glowing accents, a marquee of logos, and a hairline grid background. | 14 marquee, 13 `will-change`, 3 `mix-blend-mode`, 8 `radial-gradient` glows |
| Resend | https://www.resend.com/ | Minimal dark page that still feels expensive: soft radial light, thin borders, slow fades. | 8 `radial-gradient`, 11 `clip-path`, 8 `will-change` |
| Supabase | https://supabase.com/ | Grid plus glow, same family as Vercel but denser. | 4 `radial-gradient`, 10 `will-change`, 141 inline SVGs, 4 `clip-path` |
| Notion | https://www.notion.so/ | Typographic, illustration-led, almost no motion. | 27 inline SVGs, 1 `clip-path` |
| Awwwards health and wellness collections | https://www.awwwards.com/websites/health/ and https://www.awwwards.com/websites/wellness/ | Award galleries for health and wellness sites: the reference for what "premium" gets judged against. | category filters for Animation, Scroll, Webflow-built sites |
| Godly | https://godly.website/ | Curated showcase with an explicit "Motion" and "Animation" tag set. | tag filters for Motion, Animation, Illustration |

### The reference screenshots kept in the repo

`research/mobbin/` holds eleven Mobbin captures (each carries Mobbin's own "curated by Mobbin" watermark). They are
the evidence behind the "Inspired by" lines in section 2, so they are committed rather than left loose in the working
tree. All were captured and read on **13 November 2026**.

| File | Site | URL | What it shows |
|---|---|---|---|
| `research/mobbin/web-superpower-dark-glow-hero.webp` | Superpower | https://superpower.com/ | The dark hero: a soft amber glow behind a silhouette, one plain promise, two buttons and a three-item fact row. The model for option 6's hero. |
| `research/mobbin/web-superpower-photo-cards-with-data.webp` | Superpower | https://superpower.com/ | Photo cards that carry a number and a label - data beside the image instead of a caption. |
| `research/mobbin/web-headspace-hero-floating-characters.webp` | Headspace | https://www.headspace.com/ | Characters that float in the hero while the words stay still - "one slow thing, many quiet things". |
| `research/mobbin/web-headspace-blob-character-banner.webp` | Headspace | https://www.headspace.com/ | A blob-shaped banner that moves behind a plain line of text. |
| `research/mobbin/web-headspace-care-character-accordion.webp` | Headspace | https://www.headspace.com/ | An accordion where the open item keeps a character next to the answer. |
| `research/mobbin/web-hims-bento-treatment-cards.webp` | Hims | https://www.hims.com/ | A grid of mixed-size treatment cards (four wide, three short) - the model for option 5's bento grid. |
| `research/mobbin/ios-bevel-orb-character-checkin.webp` | Superpower (iOS) | https://superpower.com/ | A beveled orb used as a check-in control. |
| `research/mobbin/ios-brilliant-floating-orbs-loader.webp` | Superpower (iOS) | https://superpower.com/ | Floating orbs as a loading state: the calm version of a particle effect. |
| `research/mobbin/ios-insight-timer-calm-home.webp` | Superpower (iOS) | https://superpower.com/ | A quiet timer screen - the "slow breathing" reference for option 6's orb. |
| `research/mobbin/ios-opal-glowing-gem-score.webp` | Superpower (iOS) | https://superpower.com/ | A glowing gem used for a score - the "one bright object" idea. |
| `research/mobbin/ios-tolan-character-companion.webp` | Superpower (iOS) | https://superpower.com/ | A companion character that reacts to a tap. |

### The motion patterns that make these sites feel premium, and what each one costs

1. **One slow thing, many quiet things.** The premium sites move one large element (a gradient, a video, a panel) and
   keep text still. Cheap: one CSS keyframe animation, transform only.
2. **Scroll as the timeline.** Elements enter once, from a small offset, and never repeat. This is the single biggest
   "modern" signal. Cheap: CSS `animation-timeline: view()`, or one IntersectionObserver for everything.
   Support (MDN browser-compat-data, read 13 November 2026): Chrome 115+, Edge 115+, Firefox 159+, Safari 26+ -
   https://github.com/mdn/browser-compat-data/blob/main/css/properties/animation-timeline.json - so it needs a fallback
   for older browsers, which is fine, because the fallback is the same reveal.
3. **Type that reveals word by word.** A big headline where each word is masked and lifted into place. Cheap: CSS
   keyframes with a per-word delay. It is the most "startup" of the cheap effects.
4. **Gradient mesh / aurora.** Soft coloured light behind the hero. Cheap without blur filters: absolutely positioned
   `radial-gradient` circles animated with `transform` only (a blurred element re-rasterises every frame; a gradient
   does not).
5. **SVG line drawing.** An illustration that draws itself as you scrolls. Cheap: `stroke-dashoffset` animated on a
   scroll timeline. Without scroll-timeline support the line is simply already drawn.
6. **Sticky scroll storytelling.** One panel stays, the other column changes as you scroll. Cheap: `position: sticky`
   plus a scroll listener that toggles one class. **The panel has to be shorter than the space it sticks in**, or the
   browser drops the sticky offset and the panel never pins (this bit us, see Review notes).
7. **Bento grids.** Uneven cards of different sizes that lift on hover. Cheap: CSS grid spans plus a `transform`.
8. **Marquee.** A repeating row. Cheap: one keyframe translating a duplicated track; the copy is `aria-hidden` and the
   animation is paused under reduced motion.
9. **Number counters.** Numbers that count up when they enter the viewport. Cheap: one `requestAnimationFrame` loop.
   The final number stays in the HTML, so the page reads correctly without JavaScript.
10. **Magnetic buttons and card tilt.** Cursor-reactive movement. Cheap enough, but only on a fine pointer, and never
    under reduced motion.
11. **Smooth scrolling (Lenis).** Real premium sites use it (Superpower loads Lenis). We do not: it costs a library,
    it fights the browser's own scroll, and it is harder to use with a keyboard. Native scroll plus a scroll-driven
    timeline gives most of the feel for zero bytes.

### What we deliberately did not do

- **No video hero.** It is the biggest weight cost and it competes with the H1 for the LCP.
- **No 3D / WebGL.** web.dev's animations guide is the rule we follow: "An animation that moves an element using
  something other than transform is likely to be slow" and "Avoid properties that trigger layout or paint"
  (https://web.dev/articles/animations-guide, read 13 November 2026). So every animation on options 5 and 6 moves
  `transform` and `opacity` only.
- **No external motion library.** Lenis or Motion would be allowed (one small library, pinned version), but zero
  libraries is strictly better here: no CDN request, no version drift, and the whole motion layer stays tiny.
- **No parallax on text.** Parallax is applied to a decorative layer only, and is switched off on small screens.
- **Nothing that hides content behind JavaScript.** The HTML always contains the words; JavaScript only adds motion.
- **No animation under `prefers-reduced-motion: reduce`.** MDN: "Readers with vestibular motion disorders may wish to
  enable the reduce motion feature on their device before viewing the animation" - scaling or panning large objects can
  be vestibular triggers (https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion, read
  13 November 2026). On both pages the reduced-motion state is the full, static, complete page.

---
## 2. The four options

### Option 2 - Warm editorial (`2/index.html`)

- **Idea:** off-white paper, serif headlines, earth tones. Her MS story is the first thing after the hero, because it is the strongest thing about her. Reads like a magazine feature.
- **Fonts:** Fraunces (serif, 400/500/600) for headings and pull quotes, Inter for body and UI.
- **Colours:** paper `#FBF7F0`, clay `#A6573C` (hover `#8A4429`), olive `#5F6C50`, sand `#EFE3D2`, ink `#2B211C`, muted `#6B5C52`.
- **Layout:** full-bleed photo band under the headline; the story as a two-column essay with a gold-free clay pull quote; a four-step "path" timeline (MBBS to now); conditions as a two-column list with hairline rules; clay-coloured booking band with the form on paper.
- **Inspired by:** Pacific Bridge Wellness (serif reading, promise in the H1), Resilient Acupuncture (quiet, few images), Yinova Center (cream and warm accent).
- **Watch out:** a photo-led page needs real photography of the clinic later; the stock photo has to be replaced.

### Option 3 - Modern wellness (`3/index.html`)

- **Idea:** soft sage and sand, rounded shapes, gentle photos. The friendliest of the four and the easiest to read on a phone. Good if the audience skews towards women and first-time patients.
- **Fonts:** Outfit (500/600/700) for headings, Nunito Sans (400/600/700) for body.
- **Colours:** sand `#F7F2E9`, card white, sage `#E3EADF`, green `#4E6B4A` (hover `#3C5438`), peach `#F0D6C2`, ink `#2F3A33`, muted `#5E6B60`.
- **Layout:** rounded 28px image with a floating booking card; condition cards with circular number badges; step cards with peach number circles; checklist rows for "what she works with" and credentials; accordion FAQ with rounded cards; one big white booking card.
- **Inspired by:** Herb + Ohm (big warm photo, obvious booking button), Modern Acupuncture (condition-first structure), Yinova Center (soft, calm palette).
- **Watch out:** wellness styling can slide into vague. Every card here still says something concrete.

### Option 5 - Flow (`5/index.html`) - new, motion-led, light

- **Idea:** the premium-startup look. White and airy, one big confident headline that arrives word by word, a soft gradient-mesh (aurora) hero, a meridian-line illustration that draws itself as you scroll, a bento grid for conditions, and a sticky scroll story for her MS journey.
- **Fonts:** Plus Jakarta Sans (400-800, variable) for everything, Instrument Serif italic for two words of the headline and for the pull lines.
- **Colours:** white `#FFFFFF`, soft grey section `#F6F7FB`, ink `#0B1020`, muted `#5B6478`, violet `#6D5EF8`, brand `#4F46E5`, cyan `#22B8CF`, mint `#5EEAD4`, WhatsApp green `#0F7A3D`.
- **Layout:** centred hero (eyebrow pill, huge headline, sub-line, two buttons, four fact chips) over the aurora; a full-width meridian band under it; a story section that opens with the heading "How she got here", then a two-column grid: a sticky column on the left (photo + the "What she works with" panel) and five story steps on the right; a six-column bento with 2- and 3-column cards, one tall feature card and two tinted cards; three first-visit cards under a line that draws; credentials list beside the MS evidence note; two location cards; native `details` FAQ; a dark WhatsApp panel beside the form.
- **Motion (all of it, and what each one costs):**
  - Aurora: three `radial-gradient` circles drifting on `transform` only, 27-39 s loops. No blur filter, so nothing re-rasterises.
  - Headline: each word masked and lifted into place with a 60 ms stagger, CSS keyframes, under 1.1 s in total (the stagger was shortened from 80 ms in the review round so the headline is readable sooner).
  - Meridian band: an inline SVG whose paths draw themselves with `stroke-dashoffset` on a **scroll-driven** CSS timeline (`animation-timeline: view()`). `pathLength="1"` normalises every path, so one keyframe draws all of them. Without scroll-timeline support the drawing is simply already finished.
  - First-visit line: the same trick on a short SVG rule.
  - Scroll reveals: one IntersectionObserver adds `.in` to every `[data-reveal]`. A scroll sweep backs it up (anything already at or above the fold is shown), so a missed element can never stay invisible - and nothing below the fold is shown early.
  - Sticky story: `position: sticky` at `top: 88px`, capped to `max-height: calc(100vh - 104px)` with `overflow-y: auto`, plus a second observer that marks the step crossing the middle of the screen as the active one; the others sit at 55% opacity. The photo is `clamp(140px, 18vh, 240px)` so the whole column is shorter than the space it has to stick in - see Review notes, finding 1.
  - Bento hover: a 6 px lift and a gradient layer that fades in (`transform` + `opacity` only).
- **Inspired by:** Function Health (plain promise, calm grid, numbered steps), Vercel and Resend (hairline borders, radial glows, cards that lift), Stripe (gradient accents), the mixed-size treatment-card grid on Hims (`research/mobbin/web-hims-bento-treatment-cards.webp`), and the big-type-plus-italic-serif headline style that modern startup sites keep returning to.
- **Watch out:** the sticky story only works above 980px; on a phone it is a normal stacked list. The dimmed steps are 55% opacity, not 40%, so they stay readable.

### Option 6 - Pulse (`6/index.html`) - new, motion-led, dark

- **Idea:** dark, cinematic and bold, but calm - a doctor, not a nightclub. A deep near-black page with one breathing orb behind the headline, hairline grid, drifting coloured glows, a marquee of the conditions she treats, numbers that count up, and cards that tilt slightly under the pointer.
- **Fonts:** Space Grotesk (400-700, variable) for headings and UI, Inter (400-600, variable) for body text.
- **Colours:** base `#08090F`, raised surface `#12141F`, ink `#F3F5FA`, body text `#CDD2E2`, muted `#969DB2`, mint `#5EEAD4`, violet `#A78BFA`, amber `#FBBF74`, WhatsApp green `#25D366` with near-black text.
- **Layout:** centred hero over the orb; a three-number stat band (12 areas of care listed on the page, 2 places in Gurugram, 3 degrees and fellowships); the conditions marquee; a story section that opens with the heading "How she got here" and then two columns (photo + "what she works with" panel on the left, a five-step timeline on the right); a three-column conditions grid; three first-visit cards; credentials list beside the MS evidence note; two location cards; native `details` FAQ; a glass WhatsApp panel beside the form.
- **Motion (all of it, and what each one costs):**
  - Breathing orb: one blurred-free radial gradient scaling and fading on a 7 s loop, plus three "ping" rings that expand and fade on the same 7 s cycle, 2.33 s apart.
  - Glows: three large radial gradients drifting on `transform`, 30-42 s loops, plus eight small motes floating up and fading.
  - Marquee: one duplicated track translating by -50% over 42 s, edge-masked, `aria-hidden`.
  - Pulse line: an ECG-style SVG rule between the marquee and the story that draws itself on a **scroll-driven** CSS timeline, the same `stroke-dashoffset` trick as option 5.
  - Counters: `requestAnimationFrame` easing from 0 to the real number over 1.1 s when the band scrolls into view. The real numbers are in the HTML, so the page is correct without JavaScript.
  - Card tilt: pointer-driven `rotateX`/`rotateY` of at most 4-5 degrees, fine pointers only, disabled under reduced motion.
  - Reveals and the header hairline: as option 5 (same observer, same scroll sweep).
- **Inspired by:** Linear (dark, precise, product-led), Superpower (dark glow hero, layered panels - `research/mobbin/web-superpower-dark-glow-hero.webp`), Vercel (radial glows, marquee, hairline grid), Headspace (calm, friendly motion), Function Health (stat counters).
- **Watch out:** dark pages can read as less welcoming to an older first-time patient. The type is large, the copy is plain, and the WhatsApp button is the brightest thing on the page.

---

## 3. Medical and NMC compliance (why some things are deliberately missing)

Source for the rules below: **National Medical Commission, "Guidelines on Ethical Advertising and Public Communication by hospitals/medical institutions and Registered Medical Practitioners", R-13014/01/2024-Ethics**, https://nmc.org.in/whats-new/download/1874 (read 13 November 2026). Page numbers below are from that PDF.

- **No testimonials, no star ratings.** Explanation V (p.4): an RMP shall not solicit, buy, publish or share patient reviews, ratings, testimonials, endorsements or recommendations for professional promotion. So the "5.0 from 14 reviews" on the Google listing is **not** on the site. This also rules out review widgets and testimonial sections in later pages.
- **No superiority or outcome claims.** Guideline 8.1(iii) (p.8) bans "Guaranteed cures", "Best doctors", "No.1 Specialist", "100% success", "painless treatment", "Miracle treatment". Guideline 8.1(ix) bans "best", "No.1", "leading", "most trusted", "top", "number one", "unmatched". None of these words appear on any of the four pages.
- **No case studies or before/after.** Guideline 8.1(v) (p.8).
- **No prices and no offers.** The brief decides no prices on the site, and Guideline 8.1(x) (p.8) bans free procedures, discounts and anything likely to encourage unnecessary consultation.
- **Full name and qualifications on every page.** Explanation III (p.4): an RMP publishing electronic-media content should disclose name, qualifications, registration status and SMR/NMR registration number. Each page footer carries the name, all three qualifications and a line for the registration number (**to be added - Mayank or Dr. Grover**).
- **Her own photograph.** Guideline 9.2 (p.10): use of the photograph of an RMP shall not be permitted where it constitutes self-advertisement, solicitation or promotional publicity. That is why no page shows a stock person presented as her, and no page shows a photograph of her. Decide with Dr. Grover (and, if needed, a lawyer) before any photo of her goes on the site. Guideline 7.2(b) also forbids creating a synthetic person, image or endorsement.
- **Patient privacy.** Guideline 6.1 and 6.2 (p.6): patient photographs, treatment details, testimonials and before-after pictures cannot be used in advertising, and consent does not make them allowed. So: stock photos only, each captioned "Stock photo. The person shown is a model, not a patient", and no patient story on the homepage.
- **AI content.** Guideline 7.2(a) (p.6): AI-generated or AI-assisted content must not be used to create or disseminate misleading or unverifiable representations about diagnosis, treatment, outcomes, qualifications or patient experience. Guideline **7.2** (p.6) also says AI-assisted promotional content **must carry the source mark, explicitly stating that the origin of the content is AI**. Every one of the four pages now carries it, in the footer:

  > Medical information on this page was written with AI assistance and is awaiting medical review by Dr. Shruti Grover, MBBS (University of Delhi), MD Pathology (UCMS), Fellowship in Oncopathology (RGCI). It is general information, not a diagnosis. Your own plan comes after a consultation.

  The wording is **pending**, not done, because Dr. Grover has not read the copy yet. The block above is the wording from
  `strategy/plan.md` section 4.2 with the date replaced by the state of the review. When she signs the medical copy, the
  line becomes "...and reviewed by Dr. Shruti Grover ... on <date>" and the footer line "Medical review pending" is
  replaced by "Medical content reviewed by Dr. Shruti Grover - Last updated <date>".

- **Medical review date.** There is no review date yet, so the footer says "Medical review pending - Design draft, 13 November 2026". The date must be set by Dr. Grover, and re-set whenever the copy changes.
- **Motion is not advertising, but the claims are still checked.** The count-up numbers on option 6 (12, 2, 3) are counts of the items on the page itself - areas of care listed, places in Gurugram, and degrees and fellowships from the brief. They are not success rates, not patient numbers and not years of experience. Nothing on any page says she is asked about certain conditions most often: that claim is not in the brief and has no source, so the copy says "the common reasons people come in" instead.

### The MS wording (the one claim that needed care)

Every page says acupuncture for MS is **support**, never a cure, and names the limits of the evidence. Source: **Multiple Sclerosis Trust, "Acupuncture" (A-Z of MS)**, last updated 1 April 2022, https://www.mstrust.org.uk/a-z/acupuncture (read 13 November 2026), which says:

- "Acupuncture is a complementary therapy sometimes used by people with multiple sclerosis."
- "Despite some promising results, there's not enough evidence to make claims for or against the use of acupuncture in MS... However, it is generally considered safe when provided by an experienced, trained practitioner using sterile single-use needles."
- A 2014 review of 12 studies suggested possible improvement in quality of life, fatigue, spasticity and pain, "but the poor study designs made it difficult to draw any firm conclusions".
- A 2021 review found traditional and scalp acupuncture "appeared to help improve symptoms including fatigue, pain, walking difficulties and bladder problems".
- A 2018 review found "there wasn't enough evidence that acupuncture (including electroacupuncture) could reduce spasticity in MS".

So the pages promise comfort and quality of life, tell the patient to keep their neurologist, and put the source in front of them. Options 5 and 6 both carry the full evidence note, not just a link.

One headline was rewritten in the review round for this reason. Option 6 used to read **"She treats the condition she lives with."**, which is an outcome claim (8.1.vi) and contradicted the FAQ on the same page. It now reads **"A doctor who knows MS from the inside."**, and the og:description was changed to match.

---

## 4. One config place (so a move is cheap)

The brief says a location change must be cheap. Each page has a single `CLINIC` object at the bottom of the file, and
every place the page shows a location detail reads from it:

```js
var CLINIC = {
  name: 'Synergy Acupuncture Clinic',
  street: '...', city: 'Gurugram', state: 'Haryana', pincode: '122017',
  address: '...', shortAddress: 'Sector 112, Dwarka', plusCode: 'G298+88',
  hospital: 'Gajraj Hospital', hospitalAddress: 'Opposite Civil Hospital, Gurugram',
  hospitalHours: '4:00 PM - 6:00 PM',
  phone: '+917669140719', phoneDisplay: '+91 76691 40719',
  whatsapp: 'https://wa.me/917669140719', maps: '...'
};
```

**What is config-driven today, on all four pages:**

| Value | Where it appears |
|---|---|
| `name` | footer, the no-JavaScript address line |
| `address` (full) | the location card, the footer, the no-JavaScript line |
| `shortAddress` | hero sub-line, the FAQ, the booking panel |
| `plusCode` | the location card, the no-JavaScript line |
| `hospital`, `hospitalAddress`, `hospitalHours` | the location card, the FAQ, the footer, the no-JavaScript line |
| `phone`, `phoneDisplay`, `whatsapp`, `maps` | every `tel:` and `wa.me` link and the map button |
| `street`, `city`, `state`, `pincode` | the JSON-LD `PostalAddress` (options 5 and 6 rewrite the structured data from the same object at load) |

**What is NOT config-driven today, and why:**

- The `<title>`, the `<meta name="description">` and the og: tags. They are copy, and they are written by hand in the
  HTML of each file.
- The words "Gurugram" and "Dwarka" inside running prose (for example "Two places, both in Gurugram"). A move inside
  Delhi/NCR would need a copy edit for those sentences.
- The text inside `.nojs-note` (the address line for readers without JavaScript) and the JSON-LD block before the page
  runs. These are hand-written HTML: there is no build step in a design mock-up, so the no-JavaScript copy cannot be
  generated from the object at the same time.
- The `<noscript>` element was replaced by that `.nojs-note` block on purpose: the content of a `<noscript>` element is
  raw text when scripting is on, so it cannot carry the `data-clinic` hooks. The block is shown by CSS only when the
  `js` class is missing (JavaScript off) and every part of it is filled from the config when JavaScript is on.

**In the real build** (Astro on GitHub Pages) all of the above becomes one file, `src/data/clinic.json`, rendered at
build time, so crawlers and humans read the same values and there is still only one place to edit. The static
design options are the demo of that rule, not the finished mechanism.

---

## 5. Motion, weight and how it was checked

### JavaScript and page weight (measured 13 November 2026)

| Page | Inline JS (raw) | Inline JS (gzip) | External JS | HTML (raw) | HTML (gzip) | Webfont files the browser downloads (latin subset, woff2) | Images |
|---|---|---|---|---|---|---|---|
| 2 | 2,448 B | 1,120 B | none | 33,996 B | 9,550 B | Fraunces + Inter | 2 stock photos, lazy |
| 3 | 2,448 B | 1,120 B | none | 36,331 B | 10,022 B | Outfit + Nunito Sans | 2 stock photos, lazy |
| **5 Flow** | **6,456 B** | **2,280 B** | **none** | 58,872 B | 15,898 B | 54,496 B (Plus Jakarta Sans 38,812 + Instrument Serif italic 15,684) | 1 stock photo, lazy |
| **6 Pulse** | **7,832 B** | **2,688 B** | **none** | 60,321 B | 15,663 B | 70,752 B (Inter 48,432 + Space Grotesk 22,320) | 1 stock photo, lazy |

- The budget in the task is 40 KB of JavaScript per page, gzipped. Options 5 and 6 use **2.3 KB** and **2.7 KB** - about 6% of the budget - and load **no external JavaScript at all**: no jQuery, no animation library, no CDN request. Everything is CSS plus the small inline block at the bottom of each file.
- The font files are the heaviest asset. If Mayank wants the page even lighter, each page can drop to one family (option 5: Plus Jakarta Sans only, saving 16 KB; option 6: Space Grotesk only, saving 48 KB). That is the single biggest saving available and it costs one accent.
- Both pages have no hero image, so the largest contentful paint is text.

### Lighthouse, mobile, default throttling (measured 13 November 2026)

Run with Lighthouse 12.8.2 over a local HTTP server, mobile emulation (412x823), Lighthouse's default simulated Slow 4G
and 4x CPU slowdown. The numbers are kept in `website/design-options/perf-measurements.json`, and the raw Lighthouse
reports are not committed (they are about 800 KB each); the command that produced them is in that file too.

| Page | Performance | Accessibility | Best practices | SEO | LCP (3 runs) | CLS (3 runs) | FCP | TBT | Speed index |
|---|---|---|---|---|---|---|---|---|---|
| **5 Flow** | 100 | 100 | 100 | 100 | **1.0 s** (0.9-1.1) | **0.001** (0.001) | same as LCP | 0 ms | same as LCP |
| **6 Pulse** | 100 | 100 | 100 | 100 | **1.1 s** (0.9-1.1) | **0.005** (0.002-0.011) | same as LCP | 0 ms | same as LCP |

Two things had to change to get there, and both are worth keeping:

1. **The font swap was causing a layout shift of 0.107** (a whole line of the headline re-wrapped when the webfont
   arrived, pushing everything below it down). The fix is a fallback face with the same metrics: `@font-face` with
   `size-adjust` on Arial and Georgia, sized to the webfonts. The ratios were measured in Chrome on 13 November 2026
   (`scripts/tools/font-measure.html`): Plus Jakarta Sans 105% of Arial at 400 and 101% at 700-800, Instrument Serif
   italic 79% of Georgia, Space Grotesk 109% of Arial at 400 and 101% at 600, Inter 107% of Arial at 400 and 101% at
   600. With the metrics matched, the swap costs almost nothing: CLS 0.001 on option 5, 0.002-0.011 on option 6 (the last of these is the headline and
   the eyebrow letter-spacing, which no size-adjust can match exactly).
2. **The Google Fonts stylesheet was render-blocking** and Lighthouse measured LCP 2.8 s on option 5 with it. The font
   CSS is now loaded without blocking the first paint (`rel=preload` + `media="print"` + `onload`, with a
   `<noscript>` copy for readers without JavaScript). The page paints in the fallback face straight away and the
   webfont swaps in without moving much: LCP 1.0 s on option 5 and 1.1 s on option 6.

Lighthouse's simulated throttling moves a little between runs, so each page was measured three times and the table
quotes the median run with the range beside it. All three runs of both pages scored 100 in all four categories. The LCP
element is the hero sub-line on both pages (the headline itself is masked while its words fly in, so the browser does not
count it as a candidate).

The remaining Lighthouse notes are about the demo setup, not the pages: minify CSS/JS and enable compression (the real
build does both), and size the Unsplash images properly (the real build will hold its own images).

### The motion rules, and how they are kept

- **Only `transform` and `opacity` animate.** The one exception is `stroke-dashoffset` on the two SVG line drawings, which is a paint-only property and causes no layout. web.dev's animations guide: "An animation that moves an element using something other than transform is likely to be slow" (https://web.dev/articles/animations-guide, read 13 November 2026).
- **No layout shift.** Nothing animates a property that changes the size or position of other elements, and the fallback faces are metric-matched (see above). Lighthouse measures CLS 0.001 on option 5 and 0.005 (median) on option 6.
- **No JavaScript-only content.** Every word on both pages is in the HTML. The `js` class is added in `<head>`; the hidden-until-revealed state only exists when that class is present, so with JavaScript off the page is simply the static page.
- **`prefers-reduced-motion: reduce` turns the motion off completely.** The reduced-motion state is the full, static, complete page: no aurora drift, no word reveal, no scroll-driven drawing, no marquee, no counters, no tilt, no sticky-step dimming. Checked by screenshotting both pages with the media feature forced to `reduce`.
- **Mobile is simplified, not broken.** The sticky story becomes a normal list under 980px, the tilt is skipped on touch devices, the aurora is smaller, and the hero type scales with `clamp()`.

### Accessibility and layout, checked with headless Chrome (13 November 2026)

- No horizontal scroll at 390px or 1440px on any page (`scrollWidth - clientWidth = 0`, measured on all four pages at both widths).
- One `<h1>` per page; `header`, `nav`, `main`, `footer` landmarks; a skip link to `#main`. Heading order runs h1 -> h2 -> h3 with no level skipped (the story heading moved above the story columns in options 5 and 6 in the review round).
- Every image has an `alt` that describes what is in the picture; both images are below the fold with `loading="lazy"`; the hero is text, so there is no image in the LCP path.
- Form: three labelled fields (`name`, `phone`, `concern`), `autocomplete` set, and a live region for the demo reply.
- FAQ uses native `details`/`summary`, so it works without JavaScript and can be indexed.
- Focus rings on links, buttons, inputs, textareas and `summary`.
- Contrast, measured rather than guessed (ratio, AA needs 4.5): option 5 - ink on white 18.9, muted on white 5.9, muted on the grey section 5.5, link blue on white 8.5, white on the brand button 6.3, white on the WhatsApp button 5.4. Option 6 - ink on base 18.2, body text on base 13.2, muted on base 7.4, muted on a card 6.8, mint on base 13.4, dark text on the mint button 11.3, dark text on the WhatsApp green 8.4.
- Lighthouse scores 100 for accessibility on options 5 and 6.

### How the screenshots were taken

All the shots were retaken on 13 November 2026 with `scripts/tools/shots.sh` (which drives headless Chrome over the
DevTools Protocol through `scripts/tools/cdp.js`):

- The page is scrolled from top to bottom first, so every scroll reveal has played, and then back to the top before the
  capture. That is why the full-page shots show the whole page and not blank sections.
- **The 390px full-page shots are taken with the sticky WhatsApp bar hidden** (`display:none` on `.mbar`, and the body
  padding removed). A fixed bar is painted in the middle of a full-page capture, which is what made the previous
  `opt5-390.png` and `opt6-390.png` wrong.
- The `opt*-390-top.png` shots keep the bar, so they show the real phone view.
- The `opt*-1440-mid.png` and `opt*-390-mid.png` shots are taken at the story section, where the sticky column and the
  changing steps are visible.

The equivalent plain-Chrome command for a single viewport is:

```
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new \
  --screenshot=shots/opt5-1440.png --window-size=1440,900 \
  "file://$PWD/website/design-options/5/index.html"
```

---

## 6. Before this goes live

- Mayank: buy the domain (Decision in the brief), then set `CLINIC` / `clinic.json` once.
- Mayank: get the NMC registration number into the footer of every page.
- Dr. Grover: read the medical copy, then change the AI source mark from "is awaiting medical review" to "reviewed by ... on <date>" and set the review date.
- Dr. Grover + Mayank: decide the her-photo question (NMC Guideline 9.2) before any future page uses a photo of her.
- Replace the stock photos with photos of the actual clinic (nobody shows a patient).
- Decide on the form destination (WhatsApp deep link, a form service, or a Google Form for now).
- Add `Physician` / `MedicalClinic` / `FAQPage` schema from the same config file in the real build. The `Physician` schema is already in options 5 and 6; `FAQPage` is not, because it must be generated from the same content source.
- The site playbook at `/Users/knayam/Desktop/product/wt-social-robust/micro-products/research/websites-2026-11-08/site-playbook-v3.md` was read for this task (read-only, as the brief allows). It is written for app landing pages - one page per app, a keyword plan, a publishing cadence - so it was skipped here: it has no motion guidance, and its rules about app pages do not apply to a single local clinic homepage.

---

## Review notes

### Round 1 (reviewer, 13 November 2026) - `strategy/reviews/motion-r1.md`

The reviewer checked all the deliverables, re-measured the JavaScript, checked the contrast ratios by hand and marked
the pages clean on the medical side. Ten findings. Here is what was done about each one:

1. **Option 5's sticky story did not stick (major).** The column was 772px tall inside a 752px constraint rectangle, so
   Chrome dropped the offset and painted it at its flow position. Fixed: the photo is now `clamp(140px, 18vh, 240px)`,
   the column is capped at `max-height: calc(100vh - 104px)` with `overflow-y: auto` and `overscroll-behavior: contain`,
   and it sticks at `top: 88px`. Measured after the fix: the photo's top edge sits at 88px at 1440x900 and at 1366x768,
   and it stays pinned for the length of the story column. See `shots/opt5-1440-mid.png`.
2. **Option 6's H1 was an outcome claim (major).** "She treats the condition she lives with." contradicted the FAQ on
   the same page. Now "A doctor who knows MS from the inside.", with the og:description changed to match and
   "support, never a cure" kept in the sub-line.
3. **No AI source mark (major).** Guideline 7.2 requires it. All four footers now carry the block from
   `strategy/plan.md` section 4.2, worded as *pending* because Dr. Grover has not read the copy. The old
   "Medical content reviewed by Dr. Shruti Grover - Last updated 13 November 2026" line asserted a review that has not
   happened; it now says "Medical review pending - Design draft, 13 November 2026".
4. **The 390px full-page shots were wrong (major).** The fixed WhatsApp bar was painted in the middle of the page.
   All the shots were retaken; the 390px full-page shots are now taken with the bar hidden, and the notes above say so.
5. **"One config place" was not true (medium).** Three `setText()` calls matched nothing and the location strings were
   copied around the file. Now every address, hospital and hours string on all four pages reads from the `CLINIC`
   object, the JSON-LD is rewritten from it on options 5 and 6, and section 4 lists exactly what is config-driven and
   what is still hand-written copy.
6. **Unsourced popularity claims (medium).** "The problems she is asked about most often", two "Most asked about"
   tags and the counter "areas of care she is asked about most" are not in the brief and have no source. Now: "the
   common reasons people come in", the tags say what the condition is, and the counter says "areas of care listed on
   this page".
7. **LCP and CLS were asserted, not measured (medium).** Lighthouse 12.8.2, mobile, default throttling, three
   runs each: option 5 LCP 1.0 s (median) / CLS 0.001, option 6 LCP 1.1 s / CLS 0.005, all four category scores 100 in
   every run. Two real problems came
   out of the measurement and were fixed: a 0.107 layout shift from the font swap (fixed with metric-matched fallback
   faces) and a render-blocking font stylesheet that put option 5's LCP at 2.8 s (fixed by loading the font CSS without
   blocking the first paint). The method and the numbers are in section 5.
8. **Option 6's heading order (minor).** The story `<h2>` now comes above the story columns. The same fix was applied to
   option 5, which had the same h3-before-h2 problem.
9. **The Review notes section was empty (minor).** This section.
10. **Research artefacts were untracked and uncited (minor).** `research/mobbin/` (11 Mobbin captures) is now committed
    and cited in the research table in section 1, and the round summary `scripts/logs/motion-w1.txt` is committed too.
    A `.gitignore` now keeps the raw run logs and the Lighthouse reports out of the tree.

### Notes for the next reviewer

- The Lighthouse numbers come from a local HTTP server (`python3 -m http.server`), not from GitHub Pages. Real hosting
  adds TLS and CDN time, so treat 0.9 s as a floor, not a promise.
- The `size-adjust` fallback ratios were measured against Arial and Georgia on macOS. On Windows and Android the
  fallback family falls back to the same local fonts (Arial, Liberation Sans, Georgia, Times New Roman), which have
  near-identical metrics, but it is worth one check on a Windows machine.
- The sticky story still has a short travel window (the story column is about 1,000px tall and the sticky column 630px),
  so it pins for roughly a third of the section. If Mayank wants it to pin for the whole story, the photo and panel
  need to move to the right-hand column.
