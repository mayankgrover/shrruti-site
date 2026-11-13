# Homepage design options - Dr. Shruti Grover

Prepared 13 November 2026 for Mayank, to pick one direction for the clinic homepage.

- `index.html` - chooser page with the four options, in the order 2, 3, 5, 6.
- `2/index.html`, `3/index.html`, `5/index.html`, `6/index.html` - the four homepages. Each one is a single
  self-contained file: inline CSS, Google Fonts, no framework, no build step, relative links only.
- `7/index.html` - **option 7, Sunrise**, added on 13 November 2026: the illustrated and animated option (a sun that rises
  out of the clouds, a character for every condition, a companion that travels with the reader). Also one self-contained
  file, also with no framework and no build step. The chooser page is updated by the orchestrator, not by this option.
- `shots/` - full-page screenshots at 1440px and 390px, `opt*-390-top.png` (first phone screen, with the sticky
  bar in place), `opt*-1440-mid.png` and `opt*-390-mid.png` (mid-scroll, so the sticky and scroll-driven states are
  visible) and `opt*-preview.jpg` (the card image on the chooser page).
- `../../scripts/tools/cdp.js` and `../../scripts/tools/shots.sh` - the small Chrome driver used to take the shots
  and to measure the pages. No npm install needed.

Options 1 (Clinical calm) and 4 (Doctor-first authority) were **deleted on 13 November 2026**: Mayank's feedback was
"These don't look like modern options at all." They are replaced by two motion-led options, 5 (Flow) and 6 (Pulse).

All four pages carry the same facts, in the same order: header, hero, her story (MS), conditions treated, how a
first visit works, credentials, location, FAQ (4), booking (WhatsApp + form), footer, sticky "Book on WhatsApp" bar
on mobile. Option 7 carries the same facts in the same order (it has five FAQ entries instead of four, and every picture
on it is an illustration we drew rather than a stock photo).

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

### Option 7 - Sunrise (`7/index.html`) - new, illustrated and animated

The brief for this one was *the closest to Headspace*: warm yellow, orange and cream, a deep navy ink, a hero where a
smiling sun-character rises out of soft layered clouds, and a small character for every condition. It is the first option
in this repo where **every** picture is an illustration we drew as SVG - there is not one raster image or stock photo on the
page.

- **Idea:** a sunrise. The page opens on a warm yellow sky, the sun rises out of the clouds over about two seconds, and the
  rest of the page is that same sunrise told in bands: cream (her story), white (conditions), teal (a pause to breathe),
  cream (the first visit), navy (credentials and the evidence note), white (where to find her), cream (questions), and a
  yellow band that bookends the hero at the booking form.
- **Fonts:** **Figtree** (400-900, variable) for headings and UI, **Nunito** (400-800, variable) for body text. Both from
  Google Fonts, loaded without blocking the first paint, with metric-matched local fallback faces (`size-adjust`) so the
  swap costs no layout shift.
- **Colours:** sky `#FFE08A` to `#FFB02E` (the hero band), cream `#FFF6E9`, paper `#FFFDF8`, sun orange `#FF7A2F` with
  `#E85D18` for the shaded half, peach `#FFDCBF`, blush `#FFB49E`, ink navy `#16203C` (with `#2B3A5E` and `#55648A` for
  body text), teal `#3E8E82` for the breathe band and the small tags, sand `#F3E3C8` for hairlines, WhatsApp green `#25D366`.
- **Layout:** sticky header (transparent over the yellow sky, turning cream with a blur once you scroll); hero with the
  eyebrow, the headline *Feel at home in your body again.*, one line of plain English, a navy pill button, a WhatsApp
  link and three fact pills, with the sun scene beside it (below it on a phone); a navy marquee of what she treats; her
  story as a sticky illustration beside the text and the evidence note; twelve condition cards, each with its own small
  character; a teal *breathe with me* band; three first-visit cards under a dotted path with a little sun walking it; the
  credentials list beside the MS evidence note; a map illustration beside the two places; the FAQ beside a speech-bubble
  character; and the yellow booking band with the WhatsApp buttons and the short form.
- **The illustration system (52 inline SVGs, 28 KB in total):**
  - The **hero sun** is the face of the brand: a flat orange disc with closed-eye arcs, a wide smile and blush cheeks,
    a cream halo to lift it off the yellow, and four layers of cloud (two drifting back, two drifting front) that it rises
    from. Sparkles pop, two birds drift, the sun breathes and blinks.
  - **Every condition has its own character** in a cream disc: a figure bent over its lower back, a head tipping with
    tight shoulders, a shoulder with a strain mark, a leg with a lightning bolt down it, a knee with a bandage and a smile,
    two knuckles with a sparkle, a joint with creak lines, a head with a migraine spiral, a stress knot, a sleepy moon
    with a Z, a crescent moon with a flower, and the sun again with a halo for *support, not a cure*.
  - **Other scenes:** dawn hills with a walker on a path (her story), a smiley sun inside the breathing disc, a friendly
    map pin on a street map (location), the sun in a speech bubble (FAQ), and the little walking sun on the first-visit path.
  - Style rules for the whole set: flat fills only, no gradients on the characters, closed-eye smiles or dot eyes, navy
    line work, blush cheeks, and the same six colours everywhere.
- **The companion (Mayank's ask):** a small sun with a rotating ray ring sits in the right-hand lane from 1080px up and
  travels up that lane as the page goes by (a scrubbed ScrollTrigger). It waves in the hero, holds a leaf in her story,
  points at the conditions, breathes in the credentials band, holds a map pin at the location, and holds a small **Book**
  sign at the booking form. It blinks like the hero sun. A short line appears in a bubble above it when the section
  changes, and it is a WhatsApp link all the way through. On a phone it is the little sun in the sticky bottom bar, so it
  never covers a line of text.
- **Motion (all of it, and what each one costs):**
  - **Hero intro, about 3 s:** the sun rises from behind the clouds with a slight overshoot, the back clouds drift in, the
    front clouds lift, the headline and the buttons slide up in a 90 ms stagger, the sparkles pop in a 120 ms stagger, the
    birds fly in. Nothing is animated with `top`/`left`/`width`; only `transform` and `opacity`.
  - **Idle loop:** four cloud layers drift at 15-27 s, the sun breathes (1.035, 3.4 s), the sparkles twinkle, the birds
    cross, and the sun blinks every 3.4 s.
  - **Scroll-driven:** the hero scene and the hero copy drift up and fade as the hero leaves; the three hills in her-story
    illustration move at 3%, 6% and 10% (parallax) and the walker walks the path; the condition cards and their characters
    pop in; the dotted path in the first-visit section draws itself with `stroke-dashoffset` while the little sun walks it
    from step 01 to step 03; the sections, cards, FAQ rows and the form rise into place.
  - **Micro-interactions:** the buttons squish on press and spring back (elastic), the condition and step cards tilt up to
    7 degrees under the pointer (fine pointers only), and the breathe disc runs 4 seconds in and 4 seconds out with the
    label swapping between *Breathe in* and *Breathe out*.
  - **Reduced motion:** `prefers-reduced-motion: reduce` removes every timeline, every loop and every travel; the
    illustrations stay exactly where they are and the page reads as a normal page.
- **Inspired by (all read on 13 November 2026):**
  - **headspace.com** (https://www.headspace.com/) - the flat yellow band, the enormous pill button, the smiling orange
    face, the wave dividers and the scrolling line of big type. This is the structure option 7 copies.
  - **research/mobbin/motion-headspace-sun-rising-in-clouds.webp** - the exact scene in the hero: a flat sun character with
    a closed-eye smile rising out of layered clouds.
  - **research/mobbin/motion-headspace-meditation101-sun-card.webp** - the character on a rotated white card, and the warm
    layered palette.
  - **research/mobbin/motion-figma-concentric-rings-hero.webp** - the expanding rings in the breathe band.
  - **research/mobbin/motion-maxima-therapy-bold-type-character.webp** - a single bold colour field and big type.
  - **research/mobbin/motion-marshmallow-blob-eyes-logo.webp** and **web-headspace-care-character-accordion.webp** - how
    little a face needs to be to give a shape a personality.
  - **Its Nice That, Headspace overhauls visual identity to become mental health all-rounder** (25 April 2024),
    https://www.itsnicethat.com/articles/italic-studio-headspace-graphic-design-project-250424 - Headspace's orange smiley
    (inspired by meditation robes) and its breath-driven animations.
  - **Figma, Building a design system that breathes with Headspace** (6 December 2023),
    https://www.figma.com/blog/building-a-design-system-that-breathes-with-headspace/ - the same colour and motion tokens
    idea, applied here as CSS custom properties.
- **Lottie:** not used. Every animation is our own SVG plus CSS, so there is no third-party licence to record.
- **Weight (measured 13 November 2026):** the page is one HTML file, 94 KB, of which **28 KB is inline SVG** (the budget is
  120 KB). JavaScript is **50.2 KB gzipped in total**: GSAP 3.13 core 28.2 KB + ScrollTrigger 17.8 KB (both pinned to
  `cdn.jsdelivr.net/npm/gsap@3.13.0`) + the page's own script 4.2 KB. The budget is 80 KB gzipped per page. CSS is 24.8 KB
  raw / 6 KB gzipped, inline.
- **The motion recordings:** `shots/opt7-motion-390.mp4` (390x844, 20.6 s, 399 frames) and `shots/opt7-motion-1440.mp4`
  (1440x900, 23.0 s, 496 frames), with the still frames at 0 s, 1 s, 2 s, 4 s and mid-scroll next to them. They were made
  with `scripts/tools/motion.js`, which drives the same headless Chrome as `scripts/tools/cdp.js` over the DevTools
  protocol (`Page.startScreencast`) and stitches the frames with ffmpeg. No Playwright download was needed.
- **Watch out:** the hero band is a colour field, so the page has no photograph of her at all - that is deliberate (NMC
  guideline 9.2, see section 3), but it means the page has to earn trust with type, credentials and the evidence note.
  The companion's bubble is a floating layer and can sit over the right-hand gutter for a few seconds; it is
  `pointer-events: none` so it can never block a button.


### Option 8 - Qi friends (`8/index.html`) - new, illustrated and animated

The brief for this one: **playful-geometric**, the way Marshmallow, Figma and Maxima Therapy are. Cream paper, sage
green, coral and lilac blobs. The companion is a soft blob with two dot eyes, called **Qi**, and it morphs between
shapes as you scroll (circle, then a drop, then a leaf). Giant bold type, shapes that pop in, and a band of concentric
rings that expand for the "breathe with me" moment.

- **Idea:** a page of friendly shapes on cream paper, and one small character that walks the reader through it. The
  hero is a coral blob with two dot eyes and a leaf on its head, standing in front of a big sage disc with a lilac
  arch, a yellow sun, a white cloud, a checkerboard, a squiggle and a small lilac circle around it. Every band below
  keeps the same flat, outlined, sticker-like language: cream for her story, a coral marquee of what she treats,
  cream for the condition cards, a pale yellow band for the breathing rings, cream for the first visit, near-black for
  the credentials and the evidence note, cream for the location and the questions, a deep green band for booking, and
  a near-black footer.
- **Colours:** cream `#FBF3E4` (page), cream2 `#F5E9D2` (alternating bands), paper `#FFFCF5` (cards), ink `#241C12`
  (all type and all line work), ink2 `#4B4136` (body), ink3 `#6E6153` (small print), coral `#FF7A5C`, coral-deep
  `#D9452B` (the big word *inside*), coral-ink `#B33A22` (small coral kickers, 5.4:1 on cream), sage `#A9CDA0`,
  sage-2 `#7FB383`, sage-deep `#3E6B4C` (the booking band), lilac `#C6B2E8`, lilac-deep `#6B4FA8` (source links),
  sun `#FFC24A`, sun-soft `#FFE9BE` (the breathing band and the character tiles), WhatsApp green `#25D366`.
- **Fonts:** **Figtree** (variable 300-900) from Google Fonts, for the giant display type and the UI. Loaded without
  blocking the first paint, with metric-matched local fallback faces (`size-adjust` 101% at 400, 108% at 700-900) so
  the swap costs no layout shift. The ratios were measured in Chrome on 13 November 2026.
- **Layout:** sticky header (cream with a blur, a hairline once you scroll); hero with the eyebrow, the headline
  *A doctor who knows MS from the inside.*, one line of plain English, a coral pill button, a WhatsApp button and
  three fact pills, with the scene beside it (below the headline on a phone, so the scene, the headline and the button
  all fit the first screen at 390x844); a coral marquee of the conditions; her story as a drawing beside the text, the
  timeline and the evidence note; eleven condition cards, each with its own drawn character; the *breathe with me*
  band with the expanding rings; three first-visit cards with 01/02/03 in three different shapes; the credentials list
  beside the evidence note; the two places she works; four questions; and the green booking band with the WhatsApp
  buttons and the short form. A sticky *Book on WhatsApp* bar on a phone.
- **The illustration system (21 inline SVGs, 14.6 KB in total):**
  - The **hero scene** is the face of the brand: a coral blob with two dot eyes and a smile, a leaf on its head, a big
    sage disc behind it, and six flat shapes around it (lilac arch, coral circle, yellow sun, white cloud, checkerboard,
    ink squiggle, yellow leaf). The shapes pop in one after another and the blob breathes.
  - **Eleven condition characters**, one per card, in the same flat style: a red curve and a dot for low back pain, a
    figure with a spark for neck and shoulder pain, two bone ends and a worn joint for knee and joint pain, two curved
    bones for osteoarthritis, a leg with a lightning bolt for sciatica, a head with a swirl under a star for migraines, a
    leaf with a face for stress, a crescent moon with a closed eye for sleep, a five-petal flower for women's health, a
    drop with two eyes for Qi balance, and a circle with a pulse line for MS (on a lilac card, labelled *Support, not a
    cure*).
  - **Other drawings:** the story scene (two characters sitting on a green hill under a sun, with a path and a leaf),
    the two map pins for the location, the concentric rings, and Qi itself.
  - Style rules for the whole set: flat fills, a 4-5px ink outline on every shape, dot eyes or closed-eye smiles, and
    the same six colours everywhere. No gradients, no raster images, no stock photos.
- **Qi, the companion (Mayank's ask):** a sage-green blob with two dot eyes and a smile, 94px on a desktop, in the
  right-hand gutter. It stays on screen the whole way down and travels as you scroll, and it **morphs**: a circle in the
  hero and her story, a **drop** in the conditions band, a **leaf** in the breathing band and through the first visit
  and the credentials, and back to a circle at the location, the questions and the booking form. The morph is real
  geometry (GSAP MorphSVG), not a swap: the two eyes travel to their new place, the smile morphs with them, and the leaf
  grows a midrib and loses the smile. It hops when the section changes, it breathes, it blinks, and it holds a small
  **Book** sign at the booking form. One short line appears in a bubble per section ("Hello. I am Qi.", "I know MS from
  the inside too.", "Which one sounds like you?", "In for four. Out for four.", "Three steps. Nothing hidden.", "A
  pathologist first.", "Sector 112, Dwarka. See you.", "Ask me anything.", "Tap me to book on WhatsApp."); the line
  reads itself and then steps aside after about four seconds, so it never sits on the copy. Tapping Qi opens WhatsApp.
  On a phone Qi **rides in the sticky booking bar** (bottom left, next to the button), so it can never cover a line of
  text or a button.
- **Motion (all of it, and what each one costs):**
  - **Hero intro, about 2.4 s:** the eyebrow drops in, the headline rises line by line from behind its own mask, the
    scene scales up, the shapes pop in a 70 ms stagger, the character springs in, then the sub-line, the two buttons and
    the three fact pills. Only `transform` and `opacity` are animated.
  - **Idle loop:** the hero character breathes (1.035, 2.6 s) and its outline thickens by a hair, two small shapes float
    on CSS keyframes, and the marquee scrolls.
  - **Scroll-driven:** every section, card, step, question and the form rise into place once; the drawn shapes in each
    scene pop in when the drawing enters the screen; the condition cards pop in a wave; the rings expand; and Qi morphs
    and hops as the section changes.
  - **The breathing moment:** five concentric rings (coral, sun, lilac, sage, ink) around a dark centre with *Breathe
    with me* inside it. The set pulses 4 seconds in and 4 seconds out, the rings brighten in a wave, and the label under
    it swaps between *Breathe in* and *Breathe out*.
  - **Micro-interactions:** the buttons squish on press and spring back, the coral buttons pull gently towards the
    pointer (fine pointers only), the condition cards tilt with the pointer, and Qi blinks every 3.4 s.
  - **Reduced motion:** `prefers-reduced-motion: reduce` removes every timeline, every loop and the travel; the
    illustrations stay exactly where they are, Qi stays a circle in the gutter, and the page reads as a normal page.
- **Inspired by (all read on 13 November 2026):**
  - **Marshmallow** (https://marshmallow.com/) - the pink blob logo with two eyes and the heavy rounded wordmark. That is
    the whole idea of Qi: a face needs two dots and nothing else. Saved as `research/mobbin/motion-marshmallow-blob-eyes-logo.webp`.
  - **Figma** (https://www.figma.com/ and https://www.figma.com/blog/building-a-design-system-that-breathes-with-headspace/)
    - the flat geometric shapes that pop in (`research/mobbin/motion-figma-playful-shapes.webp`) and the expanding
    concentric rings (`research/mobbin/motion-figma-concentric-rings-hero.webp`), which are the breathe band here.
  - **Maxima Therapy** (https://maximatherapy.com/) - one bold colour field, enormous condensed type and a flat character
    with dot eyes (`research/mobbin/motion-maxima-therapy-bold-type-character.webp`). The coral marquee band is the same
    idea: a single flat field with very big type.
  - **headspace.com** (https://www.headspace.com/) - the level of illustration, the friendly characters and the calm pace.
  - **GSAP** (https://gsap.com/blog/3-13/) - "Thanks to Webflow GSAP is now 100% FREE including ALL of the bonus plugins
    like SplitText, MorphSVG, and all the others". That is why MorphSVG can be used here for free, pinned to
    `cdn.jsdelivr.net/npm/gsap@3.13.0`.
  - **Multiple Sclerosis Trust, "Acupuncture" (A-Z of MS)** (https://www.mstrust.org.uk/a-z/acupuncture) and the **US
    National Center for Complementary and Integrative Health, "Acupuncture: Effectiveness and Safety"**
    (https://www.nccih.nih.gov/health/acupuncture-effectiveness-and-safety) - the two sources printed on the page, next
    to the MS wording. See section 3 for why the page says *support* and never *cure*.
- **Lottie:** not used. Every animation is our own SVG, so there is no third-party licence to record.
- **Weight (measured 13 November 2026):** the page is one HTML file, **78.0 KB**, of which **14.6 KB is inline SVG** (the
  budget is 120 KB). JavaScript is **59.3 KB gzipped in total**: GSAP 3.13 core 28.2 KB + ScrollTrigger 17.8 KB +
  MorphSVGPlugin 7.5 KB (all pinned to `cdn.jsdelivr.net/npm/gsap@3.13.0`) + the page's own script 5.8 KB. The budget
  is 80 KB gzipped per page. CSS is 22.1 KB raw / 5.7 KB gzipped, inline. The page loads no images at all: there is no
  raster file anywhere, so the whole picture is 14.6 KB of vector.
- **Performance (measured 13 November 2026):** mobile 390x844 with the CDP tool's Slow 4G profile: **LCP 1.5 s** (the
  hero sub-line; the headline is masked while its lines fly in), **CLS 0**, **FCP 0.23 s**. There is no hero image at all,
  so the largest contentful paint is text.
- **Contrast (measured, not guessed):** ink on cream 15.2, body ink on cream 9.0, small print on cream 5.4, ink on the
  coral button 6.6, ink on the sage tag 9.5, cream on the ink band 15.2, the sage kicker on ink 9.5, the WhatsApp button
  8.4, the small coral kicker 5.4 and the sun kicker on the booking band 4.5. All AA.
- **The motion recordings:** `shots/opt8-motion-390.mp4` (390x844, 20.5 s, 512 frames) and
  `shots/opt8-motion-1440.mp4` (1440x900, 16.4 s, 409 frames), with the still frames at 0 s, 1 s, 2 s, 4 s and
  mid-scroll next to them (`opt8-motion-390-0s.png` and so on). They were recorded with **Playwright 1.49.1** driving
  the installed Google Chrome (`/Applications/Google Chrome.app`) with `recordVideo`, and stitched to H.264 with ffmpeg.
  The script is `scripts/tools/record-motion-playwright.js`, so the recording can be repeated:
  `node scripts/tools/record-motion-playwright.js --opt 8 --w 390 --h 844`.
- **Watch out:**
  - The page has **no photograph of her at all** - every picture is our own drawing. That is deliberate (NMC guideline
    9.2, see section 3), but it means the page has to earn trust with type, the credentials list and the evidence note.
  - Qi's bubble is a floating layer over the right-hand gutter for about four seconds at a time. It is
    `pointer-events: none`, so it can never block a button, and it hangs **under** the character rather than beside it,
    so it never lands on a heading. On a phone it is in the sticky bar instead.
  - The registration number is still a placeholder ("NMC registered - Registration number to be added"), and the form
    is a demo that is not connected to anything yet.
- **Review notes (13 November 2026):** the build was reviewed against the frames and the recordings, and these were
  fixed:
  1. **The headline never appeared.** The CSS pre-state used `translate3d(0,110%,0)`, which the browser resolves to a
     pixel value, so GSAP's `yPercent` could not reset it and the headline stayed hidden behind its own mask. The tween
     now sets both `y` and `yPercent`.
  2. **The hero buttons and pills never appeared** for the same reason: the pre-state was on the container and the tween
     was on the children. The pre-state is now on the children.
  3. **The hill in the story drawing was missing.** A shape that is scaled to zero has no box, so a ScrollTrigger placed on
     the shape itself fired at the wrong place. The trigger is now on the `<svg>` that holds the shapes, and the shapes are
     grouped by drawing.
  4. **The Qi bubble sat on the headline.** It now hangs under the character and reads itself out after four seconds.
  5. **The story hill was cut off by the edge of the drawing** and the note card covered the leaf. The hill now runs past
     the bottom edge and the note card sits under the drawing.
  6. **The small coral kicker was 3.9:1** on cream and the sun kicker on the green band was 3.8:1. Both were darkened
     to 5.4:1 and 4.5:1.
  7. **On a phone the companion sat on top of the hero button.** It now rides in the sticky booking bar instead.


---

### Option 9 - The path (`9/index.html`) - new, illustrated and animated

The brief for this one: **a scroll story through a soft landscape**. Rolling layered hills drawn in SVG with soft
gradients, a winding path, and a small character that walks the path as you scroll and passes signposts that are the
sections (her story -> conditions -> first visit -> the clinic -> book). The sky moves from dawn to a calm morning as
you go. It still has to read as a doctor's clinic: clean type panels over the scene, credentials clear.

- **Idea:** one landscape, one road, one journey. The page is not a stack of bands - it is a single 1440x900 illustrated
  world that stays fixed behind everything while the camera travels along a road. A small walker in a teal coat walks
  that road as you scroll, and six signposts along it are the six sections: **01 Story, 02 Treatments, 03 First visit,
  04 Training, 05 Clinic, 06 Book**. The signpost the walker is standing next to lights up (teal board, white label).
  The sky starts peach at dawn and cross-fades to a calm blue morning over the first half of the walk; a warm light
  overlay comes up with it. The clinic building waits at the end of the road, and the walker arrives holding a **BOOK**
  sign. All the writing sits in cream cards on the right, so the world and the walker keep the left side to themselves.
- **How the camera works (the interesting bit):** the scene is one inline SVG with `viewBox="0 0 1440 900"` and
  `preserveAspectRatio="xMidYMid slice"`, so it fills any screen without stretching. The road is a real SVG path; the
  walker's position comes from `path.getPointAtLength()` (no motion-path plugin needed), and the tangent of the road
  gives it a small lean. Five layers move at different rates (far ridge 0.16, middle ridge 0.42, near bank 0.68,
  ground 1.0, foreground 1.16) so the world has depth, and the camera follows the walker so it never runs off the screen.
  Because the SVG is scaled to the viewport, the same scene works at 390px and at 2560px without a second drawing.
- **Fonts:** **Bricolage Grotesque** (600-800, variable) for the headlines and section titles, **Figtree** (400-800,
  variable) for everything else. Both from Google Fonts, loaded without blocking the first paint, with metric-matched
  local fallback faces (`size-adjust`) so the swap costs no layout shift.
- **Colours:** dawn sky `#FFD79B` -> `#FFB69E` -> `#F7C2B4`, morning sky `#B6DCF3` -> `#CFE9E5` -> `#FFF7EA`; far ridge
  `#CBDCD8`, middle ridge `#A5C6B2`, near bank `#9CC3A6`, field `#E4EED6`; the road `#EAC99C` with a `#C79C6E` edge;
  trees `#4C8163` / `#3F7358`, bushes `#6FA186`; cream `#FFF6E9` (page), paper `#FFFCF6` (cards), ink `#1D2C2A`,
  body `#51625E`, teal `#12706B` (the coat, the buttons, the active signpost), ochre `#DE7B2C` (the scarf, the sun,
  the kickers), rose `#E98681` (the bag, the map pin), WhatsApp green `#25D366`.
- **The illustration system (18 inline SVGs, 21.5 KB in total, budget 120 KB):**
  - The **landscape**: three rolling ridges drawn as long cubic paths with vertical gradients, a field whose top edge
    follows the road, eleven trees and nine bushes placed with `<use>`, a two-stroke road, six signposts, the clinic
    building with a CLINIC signboard, and the walker.
  - The **walker** is the face of the brand: a soft teal coat, an ochre scarf, a rose satchel, a cream face with a dark
    fringe, closed-eye arcs and a small smile. It is a character, **not** a picture of Dr. Grover (NMC guideline 9.2 - see
    section 3), and nothing on the page claims that it is her.
  - **Every section gets a scene, not an icon:** her story is a microscope, a mug of tea and a plant on a desk; the
    conditions are a friendly figure with soft rings on the head, shoulders, back and knees, beside a written plan; the
    first visit is three vignettes (a clinic door, two people talking, a ticked list); training is four milestone flags
    along a path; the clinic is a small building with a map pin and a tree; the four tiles under *what she works with*
    carry a needle, a heart, a moon and two people.
- **The companion (Mayank's ask):** the walker never leaves the screen - it walks in the left lane at about 30% of the
  viewport width (27% on a phone), its legs swing only while the page is moving, it stands beside the signpost of the
  section you are reading, and at the end of the road it holds up the **BOOK** sign next to the clinic. The walker is a
  WhatsApp link: tapping it opens the booking chat, and it is a real `<a>` inside the SVG, so it works with a keyboard
  and a screen reader (`aria-label="Book a consultation on WhatsApp"`).
- **Motion (all of it, and what each one costs):**
  - **Hero intro, about 2.6 s:** the sun rises into the dawn sky, the three ridges rise from nothing in a 150 ms stagger,
    the road draws itself with `stroke-dashoffset`, the foreground bank fades up, the walker walks in from the left, and
    the hero panel and its four credential chips rise in a 90 ms stagger. Only `transform` and `opacity` are animated.
  - **Idle loop:** three clouds drift across the sky at 64-92 s, the sun's rays turn slowly (90 s), the walker's legs
    swing when you scroll, and the breathe circle runs 4 s in and 4 s out.
  - **Scroll-driven:** the camera travels along the road, the ridges and the trees drift at their own rates, the sky
    cross-fades from dawn to morning, the birds come out at half way, the signpost of the current section lights up,
    the walker's BOOK sign appears at the end, and the cards rise into place once each.
  - **Micro-interactions:** the buttons squish on press and lift on hover, the condition tiles lift 3px, the breathe
    circle runs 4 seconds in and 4 seconds out with the label swapping between *Breathe in* and *Breathe out*.
  - **Reduced motion:** `prefers-reduced-motion: reduce` removes every timeline, every loop and every travel. The
    landscape stays exactly where it is, the road is already drawn, and the page reads as a normal page.
- **Medical and NMC wording:** the same rules as options 5-8, with the wording in section 3 of this file. Acupuncture for
  MS is written as *support* only, the evidence note links to its source, there are no testimonials, no ratings, no
  before-and-after, no "best doctor" wording, no prices, no urgency and no offers, the page carries the AI source mark
  (guideline 7.2) and the medical-review-pending line, and the walker is not presented as a portrait of Dr. Grover
  (guideline 9.2). The safety line in the FAQ ("generally considered safe when it is done by an experienced, trained
  practitioner using sterile single-use needles") is taken from the NCCIH page below.
- **Inspired by (all read or checked on 13 November 2026):**
  - **research/mobbin/motion-clay-3d-landscape-hero.webp** - the soft rolling landscape with a road winding through it,
    and the way the road pulls the eye from the foreground to the horizon. This is the shape of the scene.
  - **research/mobbin/motion-mana-walking-character-hero.webp** - a big flat character that walks across a line-drawn
    landscape. This is where the companion comes from: the character walks in place while the world moves.
  - **research/mobbin/motion-headspace-sun-rising-in-clouds.webp** - the flat sun with a closed-eye smile, and the idea
    that one warm shape is enough to carry a page.
  - **research/mobbin/motion-headspace-pink-blob-bubbles.webp** - the flat shapes with no outlines on the characters, and
    the layered colour fields.
  - **headspace.com** (https://www.headspace.com/) - the friendly illustrated voice, the pill buttons, and the fact that
    every panel has a drawing rather than an icon.
  - **Multiple Sclerosis Trust, "Acupuncture" (A-Z of MS)**, https://mstrust.org.uk/a-z/acupuncture (read 13 November
    2026; the page says it was last updated 1 April 2022). The source for the evidence note: the 2014 review of 12 studies,
    the 2018 spasticity review and the 2021 review, and the rule that this site therefore writes acupuncture for MS as
    *support* and never as a cure.
  - **NCCIH, "Acupuncture: Effectiveness and Safety"**,
    https://www.nccih.nih.gov/health/acupuncture-effectiveness-and-safety (read 13 November 2026; the page says it was
    last updated October 2022). The source for the safety answer in the FAQ and for the words *sterile* and *single use*.
  - **NMC, "Guidelines on Ethical Advertising and Public Communication"**, public notice R-13014/01/2024-Ethics dated
    6 October 2026, https://nmc.org.in/whats-new/download/1874 (read 13 November 2026). The source for the AI source mark
    (7.2), the no-testimonial rule (Explanations III-V, 8.1.xi), the factual-information rule for clinical
    establishments (9.1) and the photograph rule (9.2).
  - The clinic address, the plus code and the two places come from the Google listing read on 13 November 2026 and are
    held in one config object, so a move is a one-line change.
- **Lottie:** not used. Every animation is our own SVG plus CSS, so there is no third-party licence to record.
- **Weight (measured 13 November 2026):** the page is one HTML file, 70 KB, of which **21.5 KB is inline SVG** (the budget
  is 120 KB). JavaScript is **49.3 KB gzipped in total**: GSAP 3.13 core 28.2 KB + ScrollTrigger 17.8 KB (both pinned to
  `cdn.jsdelivr.net/npm/gsap@3.13.0`) + the page's own script 3.3 KB. The budget is 80 KB gzipped per page. CSS is
  17.9 KB raw / 5.2 KB gzipped, inline. The whole HTML without CSS and JavaScript is 10.7 KB gzipped.
- **Performance (measured 13 November 2026, mobile 390x844, Slow 4G + 4x CPU):** LCP 0.32 s, CLS 0.0005, FCP 0.18 s.
  The scene is a fixed layer, so it costs no layout; the only layout shift is 0.0005, from the font swap.
- **The motion recordings:** `shots/opt9-motion-390.mp4` (390x844, 10.6 s, 91 frames) and `shots/opt9-motion-1440.mp4`
  (1440x900, 10.8 s, 74 frames), with the still frames at 0 s, 1 s, 2 s, 4 s and mid-scroll next to them. They were made
  with `scripts/tools/record-motion.js`, which drives the same headless Chrome as `scripts/tools/cdp.js` over the
  DevTools protocol and stitches the frames with ffmpeg at their real timings (a concat list with a duration per
  frame). No Playwright download was needed.
- **Watch out:** the scene is fixed, so on a very short screen the text cards cover the walker for a few seconds while a
  long card is on screen. The walker always has the left third of the desktop layout to itself; on a phone it is the
  lower part of the screen, under the card. The road is a drawn path, not a map: the address is text, and the map link
  is the one in the config.


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

### Option 7 - Sunrise (writer's own check, 13 November 2026)

Option 7 was built and checked on the same day, after the review round above. What was found and fixed, in the order it was
found (the numbers were measured with `scripts/tools/cdp.js --metrics --throttle`, the Lighthouse mobile profile):

1. **The first phone screen did not fit.** The scene, the headline and the Book button all have to be inside 390x844. The
   lede was cut to one short sentence, the fact pills were compacted (and the middle one is hidden under 520px), the hero
   scene's viewBox was cropped from 340 to 302 units, and the pill row lost 6px of margin. The scene, the headline and the
   button are now all above the fold: see `shots/opt7-390-top.png`.
2. **The sun had no eyes in the first screenshots.** The blink timeline fired on its first frame, so every screenshot
   caught it mid-blink. The first blink now waits 5.2 s.
3. **The logo read as a spiky blob at 42px.** The rays are gone; the logo is a clean smiling sun.
4. **The companion's bubble sat over the right-hand gutter.** It now sits above the character, is 172px wide at most, and
   is `pointer-events: none`, so it can never cover a button.
5. **The breathe label was printed on top of the disc.** The disc now holds the sun's face and the *Breathe in / Breathe
   out* label sits under it.
6. **The location pin sat on top of the address.** The address and the heading now keep clear of the pin.
7. **The condition cards had an empty top-right corner.** The tag (Pain, Joints, Mind, Support...) moved to the top right
   and the character grew from 74 to 84px.
8. **Her story illustration floated in the middle of a tall column.** It is now `position: sticky` at 96px on desktop, so it
   stays with the paragraph you are reading.
9. **LCP was 2.58 s.** The cause was the hero copy fading in from `opacity: 0`: the text was not painted until the animation
   ran. The copy is now painted on the first frame and slides up with a transform only (transforms do not delay LCP and do
   not shift layout). Measured after the change: **LCP 236 ms at 1440x900 and 172 ms at 390x844**, FCP 232 ms and 172 ms.
10. **CLS was 0.139.** The cause was the font swap: the three fact pills wrap to two rows in the fallback font and to one row
    in Figtree, so the hero grew by 41px when the webfont arrived and pushed the marquee and the story section down. Fixed
    three ways: the pill row reserves the height of two rows, the marquee track has a fixed height, and the header nav has a
    fixed width on wide screens. Measured after the change: **CLS 0.018 at 1440x900 and 0.000 at 390x844**.
11. **The first recording never scrolled.** The scroll script compared a `Date.now()` timestamp with the
    `requestAnimationFrame` timestamp, so the progress was always negative and the page was told to scroll to 0. Fixed by
    using `performance.now()` on both sides.
12. **The first recording was 3 fps.** Headless Chrome was launched with `--disable-gpu`, which throttled the screencast.
    Without that flag the same script records about 20 fps, and the final files are 399 frames (390px) and 496 frames
    (1440px).

Still open, on purpose:

- The companion's bubble is a floating layer. It appears for about three seconds when the section changes and it can sit
  over the empty right-hand gutter. It never blocks a click.
- The fact pills reserve two rows of height, so on a desktop there is a little extra air under them. That is the price of a
  zero-shift font swap.
- There is no photograph of her anywhere on the page. That is deliberate (NMC guideline 9.2, section 3), but it means the
  page has to earn trust with type, the credentials list and the evidence note.
- The form is a demo and sends nothing.


### Option 9 - The path (writer's own check, 13 November 2026)

Six things were wrong in the first build and were fixed before the recordings were made. They are written down because
they are the traps in this kind of page, not because anybody else will hit them.

1. **The page did not move at all.** The inline script had `defer` on it, which browsers ignore for inline scripts, so it
   ran *before* the two deferred GSAP files and bailed out. The page still looked fine, which is why it took a
   screenshot to find. The script now waits for `DOMContentLoaded` (deferred scripts have run by then) and the page
   checks `window.gsap` before it starts.
2. **The camera fought the intro.** The intro animated the same groups the camera moves, so the two overwrote each other
   and the landscape jumped. Every parallax layer now has an inner group: the camera moves the outer group, the intro
   moves the inner one.
3. **The walker stood on nothing.** `draw()` was only called when the scroll position changed, so on a page that never
   moves the walker was never placed. The scene is now drawn once at start.
4. **The signpost labels sat on top of their own number badge.** The board was too narrow and the label was centred, so
   *Treatments* ran into the badge. The boards are 180 units wide, the label is left-aligned and the words are short.
5. **The walker stood exactly on top of the signpost**, so the sign was hidden whenever it mattered. The signposts now
   stand 188 units to the side of the road, like a milestone, and the walker passes them.
6. **On a phone the hero panel was 620px tall**, which left almost no landscape on the first screen. The chips became a
   two-column grid, the lede and the buttons got smaller and the brand dropped its second line; the panel is now about
   470px, and the hero screen shows the headline, both buttons, the four credential chips, the walker and the road.

Checks that passed and needed no change: no horizontal scroll at 390px (the scene is a fixed layer with `overflow:
hidden`), every word is in the HTML (the page reads with JavaScript off; the signposts and the walker are the only things
JavaScript places, and they have a sensible position without it), the FAQ uses `<details>` so it works with a keyboard and
without JavaScript, the walker is a real link with an `aria-label`, `prefers-reduced-motion` freezes the journey at the
first signpost with the road already drawn, and the measured LCP is 0.32 s with a CLS of 0.0005 on a throttled phone.

Still open, on purpose:

- The walking character is a character, not Dr. Grover. NMC guideline 9.2 makes a photograph of the doctor on a clinic's
  own site a problem, and a cartoon of her would be the same claim in a different dress. If Mayank wants her face on the
  site, that is a decision to take with the NMC rules, not a design decision.
- The form is a demo and sends nothing.
- The Google rating (5.0 from 14 reviews, read 13 November 2026) is not on the page. A rating is factual, but it is also
  a promotional line, and guideline 8.1.xii is about ratings; leaving it off is the safer side to be wrong on.


### Notes for the next reviewer

- The Lighthouse numbers come from a local HTTP server (`python3 -m http.server`), not from GitHub Pages. Real hosting
  adds TLS and CDN time, so treat 0.9 s as a floor, not a promise.
- The `size-adjust` fallback ratios were measured against Arial and Georgia on macOS. On Windows and Android the
  fallback family falls back to the same local fonts (Arial, Liberation Sans, Georgia, Times New Roman), which have
  near-identical metrics, but it is worth one check on a Windows machine.
- The sticky story still has a short travel window (the story column is about 1,000px tall and the sticky column 630px),
  so it pins for roughly a third of the section. If Mayank wants it to pin for the whole story, the photo and panel
  need to move to the right-hand column.
