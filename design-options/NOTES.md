# Homepage design options - Dr. Shruti Grover

Prepared 13 November 2026 for Mayank, to pick one direction for the clinic homepage.

- `index.html` - chooser page with the six options, in the order 7, 8, 9, 10, 2, 3.
- `2/index.html`, `3/index.html`, `7/index.html`, `8/index.html`, `9/index.html` - five of the homepages, one file each:
  inline CSS, Google Fonts, no framework, no build step, relative links only.
- `10/index.html` - the sixth homepage. Same rules, plus `10/assets/`, the 704 KB of 3D renders it needs.
- Option 7, **Sunrise**, is the illustrated and animated option (a sun that rises out of the clouds, a character for
  every condition, a companion that travels with the reader). One self-contained file, no framework and no build step.
  The chooser page is updated by the orchestrator, not by this option.
- `shots/` - full-page screenshots at 1440px and 390px, `opt*-390-top.png` (first phone screen, with the sticky
  bar in place), `opt*-1440-mid.png` and `opt*-390-mid.png` (mid-scroll, so the sticky and scroll-driven states are
  visible) and `opt*-preview.jpg` (the card image on the chooser page).
- `../../scripts/tools/cdp.js` and `../../scripts/tools/shots.sh` - the small Chrome driver used to take the shots
  and to measure the pages. No npm install needed.

All six pages carry the same facts, in the same order: header, hero, her story (MS), conditions treated, how a
first visit works, credentials, location, FAQ, booking (WhatsApp + form), footer, sticky "Book on WhatsApp" bar
on mobile. Options 7 to 10 carry the same facts in the same order, with one difference: every picture on them is an
illustration or a 3D render we made, not a stock photo. Options 7 and 10 answer five FAQ questions, the rest answer four.

**What the review round changed (13 November 2026).** The findings are listed at the end of this file, under **Review
notes**. The big ones, across the whole set: every page now carries the NMC AI source mark, worded as *pending
review* because Dr. Grover has not read the copy yet; the 390px full-page shots are taken without the fixed WhatsApp
bar, which used to be painted in the middle of the page; the location strings are driven by one `CLINIC` object
instead of being copied around; the unsourced "most asked about" wording is gone; and LCP and CLS are measured
instead of guessed. The four illustrated options were then checked the same way, one option at a time.

## How to review

1. Open `index.html` in a browser (or serve the folder: `python3 -m http.server`).
2. Open each option on a phone (390px) and a laptop (1440px). The screenshots in `shots/` are the same thing.
3. Pick one, or say "option 2 but with option 7's motion". Mixed directions are normal and cheap to do.
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
| `research/mobbin/web-superpower-dark-glow-hero.webp` | Superpower | https://superpower.com/ | The dark hero: a soft amber glow behind a silhouette, one plain promise, two buttons and a three-item fact row. The reference for a hero built on one glowing object. |
| `research/mobbin/web-superpower-photo-cards-with-data.webp` | Superpower | https://superpower.com/ | Photo cards that carry a number and a label - data beside the image instead of a caption. |
| `research/mobbin/web-headspace-hero-floating-characters.webp` | Headspace | https://www.headspace.com/ | Characters that float in the hero while the words stay still - "one slow thing, many quiet things". |
| `research/mobbin/web-headspace-blob-character-banner.webp` | Headspace | https://www.headspace.com/ | A blob-shaped banner that moves behind a plain line of text. |
| `research/mobbin/web-headspace-care-character-accordion.webp` | Headspace | https://www.headspace.com/ | An accordion where the open item keeps a character next to the answer. |
| `research/mobbin/web-hims-bento-treatment-cards.webp` | Hims | https://www.hims.com/ | A grid of mixed-size treatment cards (four wide, three short) - the model for the bento grid of small objects. |
| `research/mobbin/ios-bevel-orb-character-checkin.webp` | Superpower (iOS) | https://superpower.com/ | A beveled orb used as a check-in control. |
| `research/mobbin/ios-brilliant-floating-orbs-loader.webp` | Superpower (iOS) | https://superpower.com/ | Floating orbs as a loading state: the calm version of a particle effect. |
| `research/mobbin/ios-insight-timer-calm-home.webp` | Superpower (iOS) | https://superpower.com/ | A quiet timer screen - the "slow breathing" reference for the breathing discs. |
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
- **No live 3D / WebGL.** web.dev's animations guide is the rule we follow: "An animation that moves an element using
  something other than transform is likely to be slow" and "Avoid properties that trigger layout or paint"
  (https://web.dev/articles/animations-guide, read 13 November 2026). So the animations on these pages are built on
  `transform` and `opacity` wherever they can be. The one exception is `stroke-dashoffset` on the drawn lines, which
  is a paint-only property and causes no layout. The 3D on option 10 is **pre-rendered** to images on this server, so
  the page ships pictures, not a 3D engine.
- **One external library, pinned.** Options 7 to 10 load GSAP 3.13 from jsdelivr with the version pinned (core and
  ScrollTrigger, plus MorphSVG on option 8). Nothing else is loaded: no jQuery, no Lenis, no Motion, no other CDN
  request. Options 2 and 3 load no library at all.
- **No parallax on text.** Parallax is applied to a decorative layer only, and is switched off on small screens.
- **Nothing that hides content behind JavaScript.** The HTML always contains the words; JavaScript only adds motion.
- **No animation under `prefers-reduced-motion: reduce`.** MDN: "Readers with vestibular motion disorders may wish to
  enable the reduce motion feature on their device before viewing the animation" - scaling or panning large objects can
  be vestibular triggers (https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion, read
  13 November 2026). On every page the reduced-motion state is the full, static, complete page.

---
## 2. The six options

The chooser page (`index.html`) shows them in the order to review them: 7, 8, 9, 10, 2, 3. They are written down here
in number order.

### Option 2 - Warm editorial (`2/index.html`)

- **Idea:** off-white paper, serif headlines, earth tones. Her MS story is the first thing after the hero, because it is the strongest thing about her. Reads like a magazine feature.
- **Fonts:** Fraunces (serif, 400/500/600) for headings and pull quotes, Inter for body and UI.
- **Colours:** paper `#FBF7F0`, clay `#A6573C` (hover `#8A4429`), olive `#5F6C50`, sand `#EFE3D2`, ink `#2B211C`, muted `#6B5C52`.
- **Layout:** full-bleed photo band under the headline; the story as a two-column essay with a gold-free clay pull quote; a four-step "path" timeline (MBBS to now); conditions as a two-column list with hairline rules; clay-coloured booking band with the form on paper.
- **Inspired by:** Pacific Bridge Wellness (serif reading, promise in the H1), Resilient Acupuncture (quiet, few images), Yinova Center (cream and warm accent).
- **Watch out:** a photo-led page needs real photography of the clinic later; the stock photo has to be replaced.

### Option 3 - Modern wellness (`3/index.html`)

- **Idea:** soft sage and sand, rounded shapes, gentle photos. The friendliest of the six and the easiest to read on a phone. Good if the audience skews towards women and first-time patients.
- **Fonts:** Outfit (500/600/700) for headings, Nunito Sans (400/600/700) for body.
- **Colours:** sand `#F7F2E9`, card white, sage `#E3EADF`, green `#4E6B4A` (hover `#3C5438`), peach `#F0D6C2`, ink `#2F3A33`, muted `#5E6B60`.
- **Layout:** rounded 28px image with a floating booking card; condition cards with circular number badges; step cards with peach number circles; checklist rows for "what she works with" and credentials; accordion FAQ with rounded cards; one big white booking card.
- **Inspired by:** Herb + Ohm (big warm photo, obvious booking button), Modern Acupuncture (condition-first structure), Yinova Center (soft, calm palette).
- **Watch out:** wellness styling can slide into vague. Every card here still says something concrete. One open item:
  the pull quote still reads "She treats the condition she lives with", the exact line the review round rewrote
  elsewhere as an outcome claim (see section 3). It should be reworded if this option is picked; the option files were
  not touched in this pass.

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
  body text), teal `#3E8E82` for the small tags and the darker `#2C6B62` for the breathe band, sand `#F3E3C8` for
  hairlines, WhatsApp green `#25D366`. Text orange is `#B2470F`: `#E85D18` on cream measured 3.26:1, so it is only
  used for fills now.
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
- **Free assets (3D models, stock photos):** not used. Option 7 draws everything itself, so there is no third-party
  licence to record, no `credits.jsonl` and no credit line in the footer. The task file allows a pre-rendered 3D cloud
  scene here, but the hand-drawn SVG clouds are the same idea, weigh 0 KB to download and can be animated frame by frame,
  which a still cannot.
- **Weight (measured 13 November 2026, after the round-2 fixes):** the page is one HTML file, 97.1 KB, of which
  **28.7 KB is inline SVG** in 52 blocks (the budget is 120 KB). JavaScript is **50.6 KB gzipped in total**: GSAP 3.13 core
  28.2 KB + ScrollTrigger 17.8 KB (both pinned to `cdn.jsdelivr.net/npm/gsap@3.13.0`) + the page's own script 4.6 KB.
  The budget is 80 KB gzipped per page. CSS is 27.0 KB raw / 6.8 KB gzipped, inline.
- **Speed (measured 13 November 2026, Lighthouse mobile profile: 4x CPU, Slow 4G, after the round-2 fixes):** LCP
  **216 ms at 1440x900** and **212 ms at 390x844**; CLS **0.018 at 1440x900** and **0.000 at 390x844**; FCP 216 ms and
  212 ms. The small desktop shift is the webfont swap moving the header links sideways; see the review notes below.
- **The motion recordings:** `shots/opt7-motion-390.mp4` (390x844, 18.21 s, 1070 frames) and
  `shots/opt7-motion-1440.mp4` (1440x900, 18.27 s, 1077 frames), with the still frames at 0 s, 1 s, 2 s, 4 s and
  mid-scroll next to them (`-f0s.png`, `-f1s.png`, `-f2s.png`, `-f4s.png`, `-mid.png`). They were made with
  `scripts/tools/motion.js`, which drives the same headless Chrome as `scripts/tools/cdp.js` over the DevTools
  protocol (`Page.startScreencast`) and stitches the frames with ffmpeg. The stills are cut out of the finished video
  with `select=gte(t,T)`, which decodes in order and takes the first frame at or after the wanted second, and the
  seconds are counted from the marker the page writes when the intro starts (`window.__introT`), so the frames are the
  intro and not a later moment. No Playwright download was needed. Each recording leaves a small `-meta.json` next to
  it, so the still frames can be cut again at any other moment.
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
- **It reads without JavaScript:** every word is in the HTML, the walker and the six signposts have a hand-written
  place in the markup that the script then replaces with an exact one, and if the GSAP files never arrive the page still
  shows the whole landscape, the road, the walker and the first signpost. Only the camera and the sky are missing.
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
- **Medical and NMC wording:** the same rules as options 7 and 8, with the wording in section 3 of this file. Acupuncture for
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
- **Weight (measured 13 November 2026):** the page is one HTML file, 70.5 KB, of which **21.9 KB is inline SVG** (the budget
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


### Option 10 - Soft 3D (`10/index.html`) - new, illustrated and animated

Mayank's note (13 November 2026): option 7 (a flat Headspace sun, warm yellow) and option 8 (a flat blob character,
cream and coral) looked "borderline the same". Option 9 is a storybook landscape with a walking character. Option 10 is
the one that is **drastically different** from all three: a real 3D render, a centred hero, a bento grid and a
scroll-scrubbed scene.

- **Idea:** one matte 3D companion - a lilac pebble with two gentle eyes and a white halo ring - floats above the
  headline in a centred, full-bleed hero. Below it, a bento grid where every condition has its own small 3D object,
  glass cards, and a "first visit" section whose scene is a real 3D still life that turns as the reader scrolls.
  No marquee strip, no headline-left/illustration-right split.
- **Everything on the page is a real 3D render.** There is no flat illustration on this page: the companion, the
  fourteen condition objects, the certificate, the two location drawings and the twenty-four frames of the scroll
  scene were all rendered on this server with **67.js 0.16.0** from procedural scene recipes (lathe, sphere, torus,
  curve, box, cylinder - no downloaded models), lit with a three-point studio rig and keyed off a flat magenta card
  to a transparent WebP. The recipes are in `scripts/render/67-opt10.mjs`; the keying, cropping and encoding are in
  `scripts/render/postprocess-opt10.sh` and `scripts/render/alpha-bbox.py`. Every asset is listed in
  `10/assets/credits.jsonl` (all of them made for this project, so no third-party credit is owed).
- **Fonts:** Inter Tight (400/500/600/700), a clean modern grotesk - not the rounded Headspace face, which options 7
  and 8 use.
- **Colours:** paper `#FBF9F5`, ink `#221C30`, lilac `#C9B8F2`, deep lilac `#5B3FA0`, mint `#A9E3CE`, sky
  `#AECBEF`, peach `#F8C9A9`, rose `#F6B9C9`, one dark band `#241D33` for the evidence note.
- **Layout:** centred hero (eyebrow, the 3D companion, the headline, the lede, two buttons, four fact chips) - no
  marquee; a "breathe with me" band; her story with a sticky 3D companion card; the bento grid of nine condition
  tiles plus a purple "not sure which one is yours?" WhatsApp card; the scroll-scrubbed "first visit" scene with
  three steps and a progress bar; the dark evidence band with the sources; credentials; two locations; the FAQ; the
  booking section (WhatsApp + the short form); the footer; the sticky mobile bar.
- **Motion:**
  - The hero intro is drawn in CSS (`html.js` rules), so the first frame and the animation start in the same place:
    the companion rises and fades in over 0.85 s, the eyebrow, headline, lede, buttons and chips rise in turn. The
    **text is painted on the first frame** and only moves with a transform, so the page is never an empty box and the
    headline is not held back from the LCP.
  - After the intro the companion floats: a 7.5 s `translateY` + `rotate` loop, transform only.
  - The **first visit scene is scrubbed by the scroll**: 24 real 3D frames of a table-top still life (the companion,
    two pebbles and a single needle on a soft round mat) with the camera arcing around it. GSAP 3.13 ScrollTrigger
    (`scrub: 0.45`) advances the frames, with a plain scroll-listener fallback if the library does not load.
  - A progress bar and a "Step 2 of 3" label follow the scroll; each step card lights up as it reaches the middle of
    the screen, and on a phone the scene jumps to the frame for the step you are on.
  - The **companion travels with the reader**: it is fixed in the bottom corner, it rises as you read, it says a
    different line for each section, and tapping it opens WhatsApp. On a phone it sits inside the sticky bar so it can
    never cover a line of text or a button.
  - "Breathe with me" is a 8 s CSS scale loop (4 s in, 4 s out) with a label that changes with it.
  - The condition tiles lift and tilt a few degrees under the pointer, on fine pointers only.
- **References used (read 13 November 2026):** `research/mobbin/ios-bevel-orb-character-checkin.webp` (the halo orb
  this page is modelled on), `research/mobbin/web-hims-bento-treatment-cards.webp` (the bento grid of small 3D
  objects), `research/mobbin/ios-opal-glowing-gem-score.webp` (one bright object as the hero) and
  `research/mobbin/motion-clay-3d-landscape-hero.webp` (the soft matte clay look).
- **Weight:** the whole asset folder is 704 KB, of which 372 KB is the 24-frame scroll sequence (about 15 KB a
  frame) and 224 KB is the 6 second WebM loop. The page itself loads one 19 KB still for the hero and the frames it
  needs.
  **JavaScript (measured 13 November 2026):** GSAP 3.13.0 is 72,435 bytes raw / 28,208 bytes gzipped and
  ScrollTrigger 3.13.0 is 44,157 bytes raw / 17,820 bytes gzipped, both from jsdelivr and pinned. Our own inline
  script is 12.7 KB raw (about 3.5 KB gzipped). Total about 49 KB gzipped, inside the 80 KB budget. There is no
  inline SVG illustration on this page at all - every picture is a 3D render - so the SVG budget is unused. The rest
  of the motion is CSS. The Google Fonts stylesheet is a normal, render-blocking `<link>`, which is deliberate here:
  it means the webfont is in place before the first paint, so the headline never reflows when it arrives. Measured on
  a throttled phone (Slow 4G, 4x CPU): **CLS 0.000**.
- **Watch out:** the alpha channel of a VP9 WebM cannot be muxed by the ffmpeg on this server (the WebM muxer does not
  write the alpha flag), so the hero uses the still plus a CSS float and the WebM is shipped as the loop export
  rather than as a `<video>`. The 24 scrub frames are the real 3D motion on this page.


## 3. Medical and NMC compliance (why some things are deliberately missing)

Source for the rules below: **National Medical Commission, "Guidelines on Ethical Advertising and Public Communication by hospitals/medical institutions and Registered Medical Practitioners", R-13014/01/2024-Ethics**, https://nmc.org.in/whats-new/download/1874 (read 13 November 2026). Page numbers below are from that PDF.

- **No testimonials, no star ratings.** Explanation V (p.4): an RMP shall not solicit, buy, publish or share patient reviews, ratings, testimonials, endorsements or recommendations for professional promotion. So the "5.0 from 14 reviews" on the Google listing is **not** on the site. This also rules out review widgets and testimonial sections in later pages.
- **No superiority or outcome claims.** Guideline 8.1(iii) (p.8) bans "Guaranteed cures", "Best doctors", "No.1 Specialist", "100% success", "painless treatment", "Miracle treatment". Guideline 8.1(ix) bans "best", "No.1", "leading", "most trusted", "top", "number one", "unmatched". None of these words appear on any of the six pages.
- **No case studies or before/after.** Guideline 8.1(v) (p.8).
- **No prices and no offers.** The brief decides no prices on the site, and Guideline 8.1(x) (p.8) bans free procedures, discounts and anything likely to encourage unnecessary consultation.
- **Full name and qualifications on every page.** Explanation III (p.4): an RMP publishing electronic-media content should disclose name, qualifications, registration status and SMR/NMR registration number. Each page footer carries the name, all three qualifications and a line for the registration number (**to be added - Mayank or Dr. Grover**).
- **Her own photograph.** Guideline 9.2 (p.10): use of the photograph of an RMP shall not be permitted where it constitutes self-advertisement, solicitation or promotional publicity. That is why no page shows a stock person presented as her, and no page shows a photograph of her. Decide with Dr. Grover (and, if needed, a lawyer) before any photo of her goes on the site. Guideline 7.2(b) also forbids creating a synthetic person, image or endorsement.
- **Patient privacy.** Guideline 6.1 and 6.2 (p.6): patient photographs, treatment details, testimonials and before-after pictures cannot be used in advertising, and consent does not make them allowed. So: stock photos only, each captioned "Stock photo. The person shown is a model, not a patient", and no patient story on the homepage.
- **AI content.** Guideline 7.2(a) (p.6): AI-generated or AI-assisted content must not be used to create or disseminate misleading or unverifiable representations about diagnosis, treatment, outcomes, qualifications or patient experience. Guideline **7.2** (p.6) also says AI-assisted promotional content **must carry the source mark, explicitly stating that the origin of the content is AI**. Every page now carries it, in the footer:

  > Medical information on this page was written with AI assistance and is awaiting medical review by Dr. Shruti Grover, MBBS (University of Delhi), MD Pathology (UCMS), Fellowship in Oncopathology (RGCI). It is general information, not a diagnosis. Your own plan comes after a consultation.

  The wording is **pending**, not done, because Dr. Grover has not read the copy yet. The block above is the wording from
  `strategy/plan.md` section 4.2 with the date replaced by the state of the review. When she signs the medical copy, the
  line becomes "...and reviewed by Dr. Shruti Grover ... on <date>" and the footer line "Medical review pending" is
  replaced by "Medical content reviewed by Dr. Shruti Grover - Last updated <date>".

- **Medical review date.** There is no review date yet, so the footer says "Medical review pending - Design draft, 13 November 2026". The date must be set by Dr. Grover, and re-set whenever the copy changes.
- **Motion is not advertising, but the claims are still checked.** The numbers a page shows are counts of the items on that page - the areas of care listed, the places in Gurugram, and the degrees and fellowships from the brief. They are not success rates, not patient numbers and not years of experience. Nothing on any page says she is asked about certain conditions most often: that claim is not in the brief and has no source, so the copy says "the common reasons people come in" instead.

### The MS wording (the one claim that needed care)

Every page says acupuncture for MS is **support**, never a cure, and names the limits of the evidence. Source: **Multiple Sclerosis Trust, "Acupuncture" (A-Z of MS)**, last updated 1 April 2022, https://www.mstrust.org.uk/a-z/acupuncture (read 13 November 2026), which says:

- "Acupuncture is a complementary therapy sometimes used by people with multiple sclerosis."
- "Despite some promising results, there's not enough evidence to make claims for or against the use of acupuncture in MS... However, it is generally considered safe when provided by an experienced, trained practitioner using sterile single-use needles."
- A 2014 review of 12 studies suggested possible improvement in quality of life, fatigue, spasticity and pain, "but the poor study designs made it difficult to draw any firm conclusions".
- A 2021 review found traditional and scalp acupuncture "appeared to help improve symptoms including fatigue, pain, walking difficulties and bladder problems".
- A 2018 review found "there wasn't enough evidence that acupuncture (including electroacupuncture) could reduce spasticity in MS".

So the pages promise comfort and quality of life, tell the patient to keep their neurologist, and put the source in front of them. Every option carries the full evidence note, not just a link.

One headline was rewritten in the review round for this reason. It used to read **"She treats the condition she lives with."**, which is an outcome claim (8.1.vi) and contradicted the FAQ on the same page. It now reads **"A doctor who knows MS from the inside."**, and the og:description was changed to match.

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

**What is config-driven today, on all six pages:**

| Value | Where it appears |
|---|---|
| `name` | footer, the no-JavaScript address line |
| `address` (full) | the location card, the footer, the no-JavaScript line |
| `shortAddress` | hero sub-line, the FAQ, the booking panel |
| `plusCode` | the location card, the no-JavaScript line |
| `hospital`, `hospitalAddress`, `hospitalHours` | the location card, the FAQ, the footer, the no-JavaScript line |
| `phone`, `phoneDisplay`, `whatsapp`, `maps` | every `tel:` and `wa.me` link and the map button |
| `street`, `city`, `state`, `pincode` | the JSON-LD `PostalAddress` (options 7, 8 and 10 rewrite the structured data from the same object at load; options 2, 3 and 9 write it by hand) |

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

| Page | Page file | JavaScript (gzip) | External JS | Webfont files the browser downloads (latin subset, woff2) | Images |
|---|---|---|---|---|---|
| 2 Warm editorial | 33,996 B HTML (9,550 B gzip) | 1,120 B inline | none | Fraunces + Inter | 2 stock photos, lazy |
| 3 Modern wellness | 36,331 B HTML (10,022 B gzip) | 1,120 B inline | none | Outfit + Nunito Sans | 2 stock photos, lazy |
| 7 Sunrise | 97.1 KB HTML, of which 28.7 KB is inline SVG | 50.6 KB in total: GSAP core 28.2 + ScrollTrigger 17.8 + the page's own 4.6 | GSAP 3.13 from jsdelivr, pinned | Figtree + Nunito | none (all SVG) |
| 8 Qi friends | 78.0 KB HTML, of which 14.6 KB is inline SVG | 59.3 KB in total: GSAP core 28.2 + ScrollTrigger 17.8 + MorphSVG 7.5 + the page's own 5.8 | GSAP 3.13 from jsdelivr, pinned | Figtree | none (all SVG) |
| 9 The path | 70.5 KB HTML, of which 21.9 KB is inline SVG | 49.3 KB in total: GSAP core 28.2 + ScrollTrigger 17.8 + the page's own 3.3 | GSAP 3.13 from jsdelivr, pinned | Bricolage Grotesque + Figtree | none (all SVG) |
| 10 Soft 3D | 71.5 KB page file, plus 704 KB of assets | about 49 KB: GSAP core 28.2 + ScrollTrigger 17.8 + the page's own 3.5 | GSAP 3.13 from jsdelivr, pinned | Inter Tight | 3D renders: a 19 KB hero still, 24 scrub frames, a 224 KB WebM loop |

- The budget for the illustrated options is 80 KB of JavaScript per page, gzipped, GSAP included
  (`scripts/tasks/05-design-illustrated.md`). All four sit inside it, at 49-59 KB. Options 2 and 3 load **no external
  JavaScript at all**: no jQuery, no animation library, no CDN request. Everything there is CSS plus a small inline
  block of vanilla JavaScript.
- Options 7, 8 and 9 load **no image files at all**. Every picture is inline SVG, so the whole page is text and vectors.
  Option 10 is the only page with image files, and every one of them is a render made for this project.
- The font files are the heaviest asset on options 2 and 3. If Mayank wants those pages lighter, each can drop to one
  family. That is the single biggest saving available and it costs one accent.

### Speed, measured on a throttled phone (13 November 2026)

Measured with `scripts/tools/cdp.js --metrics --throttle` on a 390x844 viewport with the Slow 4G profile and a 4x CPU
slowdown. Option 7 was measured with Lighthouse 12.8.2 on the same profile, and gave the same numbers.

| Page | LCP | CLS | FCP | How it was measured |
|---|---|---|---|---|
| 2 Warm editorial | 0.42 s | 0.016 | 0.42 s | CDP tool, mobile 390x844; the one shift is in the hero, when the webfont arrives |
| 3 Modern wellness | 0.39 s | 0.002 | 0.39 s | CDP tool, mobile 390x844 |
| 7 Sunrise | 0.21 s | 0.000 | 0.21 s | Lighthouse 12.8.2, mobile profile; 0.22 s and CLS 0.018 at 1440x900 |
| 8 Qi friends | 1.5 s | 0 | 0.23 s | CDP tool, mobile 390x844; the headline is masked while its lines fly in, so the sub-line is the LCP |
| 9 The path | 0.32 s | 0.0005 | 0.18 s | CDP tool, mobile 390x844; the scene is a fixed layer, so it costs no layout |
| 10 Soft 3D | 0.95 s | 0.000 | 0.48 s | CDP tool, throttled phone (Slow 4G, 4x CPU) |

Two things had to change to get there, and both are worth keeping:

1. **The font swap was causing a layout shift of 0.107** (a whole line of the headline re-wrapped when the webfont
   arrived, pushing everything below it down). The fix is a fallback face with the same metrics: `@font-face` with
   `size-adjust` on Arial and Georgia, sized to the webfonts. The ratios were measured in Chrome on 13 November 2026
   (`scripts/tools/font-measure.html`). With the metrics matched, the swap costs almost nothing: the measured CLS is
   0.000 to 0.018 across the six pages.
2. **The Google Fonts stylesheet was render-blocking**, and Lighthouse measured LCP 2.8 s on one page with it. The font
   CSS is now loaded without blocking the first paint (`rel=preload` + `media="print"` + `onload`, with a
   `<noscript>` copy for readers without JavaScript). The page paints in the fallback face straight away and the
   webfont swaps in without moving much. Options 7, 8 and 9 do this. Option 10 keeps the stylesheet render-blocking on
   purpose: the headline there must not reflow when the font arrives, and the measured CLS is 0.000.

The numbers move a little between runs, so each page was measured more than once and the table quotes the run that was
kept. The remaining notes are about the demo setup, not the pages: minify CSS/JS and enable compression (the real build
does both), and size the stock photos properly (the real build will hold its own images).

### The motion rules, and how they are kept

- **Only `transform` and `opacity` animate.** The one exception is `stroke-dashoffset` on the drawn lines (the dotted path on option 7, the road on option 9), which is a paint-only property and causes no layout. web.dev's animations guide: "An animation that moves an element using something other than transform is likely to be slow" (https://web.dev/articles/animations-guide, read 13 November 2026).
- **No layout shift.** Nothing animates a property that changes the size or position of other elements, and the fallback faces are metric-matched (see above). The measured CLS is 0.000 to 0.018 across the six pages.
- **No JavaScript-only content.** Every word is in the HTML. The `js` class is added in `<head>`; the hidden-until-revealed state only exists when that class is present, so with JavaScript off the page is simply the static page. Option 9 goes further: it says so in writing, and the landscape, the road, the walker and the first signpost all have a hand-written place in the markup.
- **`prefers-reduced-motion: reduce` turns the motion off completely.** The reduced-motion state is the full, static, complete page: no sunrise intro, no drifting clouds, no scroll-driven drawing, no marquee, no tilt, no travelling companion. Checked by screenshotting with the media feature forced to `reduce`.
- **Mobile is simplified, not broken.** The tilt is skipped on touch devices, the illustrations scale down, the hero type scales with `clamp()`, and the companion moves into the sticky booking bar so it can never cover a line of text.

### Accessibility and layout, checked with headless Chrome (13 November 2026)

- No horizontal scroll at 390px or 1440px on any page (`scrollWidth - clientWidth = 0`, measured on all six pages at both widths).
- One `<h1>` per page; `header`, `nav`, `main`, `footer` landmarks; a skip link to `#main`. Heading order runs h1 -> h2 -> h3 with no level skipped.
- Every image has an `alt` that describes what is in the picture; on options 2 and 3 both images are below the fold with `loading="lazy"`. Options 7, 8 and 9 have no image files at all, only inline SVG. On option 10 the images are decorative renders next to the words, so they carry an empty `alt` and the copy beside them carries the meaning; the small hero still is the only one loaded eagerly.
- Form: three labelled fields (`name`, `phone`, `concern`), `autocomplete` set, and a live region for the demo reply.
- FAQ uses native `details`/`summary`, so it works without JavaScript and can be indexed.
- Focus rings on links, buttons, inputs, textareas and `summary`.
- Contrast, measured rather than guessed (ratio, AA needs 4.5): option 7 - the text orange on cream 5.16, white on the teal band 6.20. Option 8 - ink on cream 15.2, body ink on cream 9.0, small print on cream 5.4, ink on the coral button 6.6, the sage kicker on ink 9.5, the WhatsApp button 8.4, the coral kicker 5.4, the sun kicker on the booking band 4.5. All AA.
- Lighthouse scores 100 for accessibility on the pages it was run on, and the same checks (landmarks, heading order, form labels, focus rings, contrast) were made by hand on the ones it was not.

### How the screenshots were taken

All the shots were retaken on 13 November 2026 with `scripts/tools/shots.sh` (which drives headless Chrome over the
DevTools Protocol through `scripts/tools/cdp.js`):

- The page is scrolled from top to bottom first, so every scroll reveal has played, and then back to the top before the
  capture. That is why the full-page shots show the whole page and not blank sections.
- **The 390px full-page shots are taken with the sticky WhatsApp bar hidden** (`display:none` on `.mbar`, and the body
  padding removed). A fixed bar is painted in the middle of a full-page capture, which is what made the first batch of
  phone shots wrong.
- The `opt*-390-top.png` shots keep the bar, so they show the real phone view.
- The `opt*-1440-mid.png` and `opt*-390-mid.png` shots are taken at the story section, where the sticky column and the
  changing steps are visible.

The equivalent plain-Chrome command for a single viewport is (the browser on this server is Playwright's Chromium):

```
"/home/ubuntu/.cache/ms-playwright/chromium-1243/chrome-linux64/chrome" --headless=new \
  --screenshot=shots/opt7-1440.png --window-size=1440,900 \
  "file://$PWD/website/design-options/7/index.html"
```

---

## 6. Before this goes live

- Mayank: buy the domain (Decision in the brief), then set `CLINIC` / `clinic.json` once.
- Mayank: get the NMC registration number into the footer of every page.
- Dr. Grover: read the medical copy, then change the AI source mark from "is awaiting medical review" to "reviewed by ... on <date>" and set the review date.
- Dr. Grover + Mayank: decide the her-photo question (NMC Guideline 9.2) before any future page uses a photo of her.
- Replace the stock photos with photos of the actual clinic (nobody shows a patient).
- Decide on the form destination (WhatsApp deep link, a form service, or a Google Form for now).
- Add `Physician` / `MedicalClinic` / `FAQPage` schema from the same config file in the real build. The `Physician` schema is already in all six options, and `FAQPage` is in option 9; the rest has to be generated from the same content source.
- The site playbook at `/work/distribution/micro-products/research/websites-2026-11-08/site-playbook-v3.md` was read for this task (read-only, as the brief allows). It is written for app landing pages - one page per app, a keyword plan, a publishing cadence - so it was skipped here: it has no motion guidance, and its rules about app pages do not apply to a single local clinic homepage.

---

## Review notes

Each option was built, opened in a browser, filmed, and then fixed. What was found is written down under each option:
what broke, why it broke, and what the number was after the fix. The rule is the same for all of them - a page is not
finished until it has been looked at in the browser at 390px and at 1440px, with the motion running and with the motion
switched off.

### Option 7 - Sunrise (writer's own check, 13 November 2026)

Option 7 was built and checked on the same day. What was found and fixed, in the order it was
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

14. **The still frames were taken with `Page.captureScreenshot`, which lands a second or two late.** That is why every
    early screenshot showed the intro already finished. The frames are now cut out of the finished video at the exact
    second, timed from a marker the page writes when the intro starts (`window.__introT`). `ffmpeg -ss` on the
    variable-frame-rate recording landed on the wrong frame (the 2 s and 4 s stills of the 1440 s run were already
    scrolled), so the stills are cut with `select=gte(t,T)` instead: it decodes in order and takes the first frame at or
    after the wanted second. In the round-2 recordings the 0 s frame is the first frame of the intro (the sun is still a
    pale disc low in the sky), the 1 s frame has the sun up with its face and the clouds in place, the 2 s frame has the
    sparkles and the birds, and the 4 s frame is the idle loop.
15. **The first scroll-through started while the intro was still playing**, so the video never showed the intro properly.
    The recorder now waits for the intro marker, lets the whole 4 s intro play, and only then scrolls.
16. **The page flashed with the sun already up before the animation began**, because the first frame of the intro was set
    by GSAP, which arrives from the CDN a moment after the first paint. The first frame is now drawn in CSS (`html.js`
    rules) so the page and the timeline start from exactly the same place.
17. **The wide multiple-sclerosis card had a small character floating in a lot of white space.** On that card the character
    now floats to the right and the copy has the room.


18. **Checked without JavaScript and with reduced motion.** With script execution disabled the page still reads as a
    normal page: the sun is up, the headline is in place, every word is there (the intro's first frame is drawn in CSS, and
    the `js` class is never added, so nothing can be left hidden). With `prefers-reduced-motion: reduce` every timeline,
    loop and travel is skipped, the marquee stops, the breathe disc holds still, and the illustrations stay where they are.
    Both were taken with headless Chrome (`scripts/tools/cdp.js --reduce`, and a run with
    `Emulation.setScriptExecutionDisabled`).

### Option 7 - Sunrise, round 2 (writer, 13 November 2026, after `strategy/reviews/opt7-r1.md`)

The reviewer's round-1 findings (`strategy/reviews/opt7-r1.md`) were fixed one at a time, the page was re-shot and the
recordings were re-cut. Only `website/design-options/7/` and `shots/opt7-*` were touched.

1. **Her name and her qualifications were missing on every phone.** One rule (`.brand span{display:none}` under 430px)
   hid the whole text block, in the header *and* in the footer, so a 390px visitor saw an orange disc with no name and no
   degrees. The rule now hides only the tagline, the header is a little smaller on a phone so the name and the Book
   button both fit, and the footer block wraps instead of being cut off. The footer brand link also got an
   `aria-label`, because it had no accessible name of its own.
2. **Text colours failed WCAG AA.** `#E85D18` on cream measured 3.26:1 and the white copy on the teal band measured
   3.29:1. Text orange is now `#B2470F` (5.16:1 on cream) and the breathe band is `#2C6B62` (white 6.20:1, body copy
   5.24:1). The bright orange and the mid teal are still used for fills.
3. **The sparkles were all drawn in the top-left corner of the hero.** `transform-box: fill-box` on an SVG shape makes
   the browser measure GSAP's transform origin from the shape a second time, so every scaled shape jumped to the origin
   of the drawing: a white sliver sat on the yellow field and the four sparkles were never seen. The rule is gone, GSAP
   sets the sparkles' first frame, and they now sit where they were designed (`shots/opt7-390-top.png`).
4. **The still frames did not prove the motion** (item 14 above). All ten stills were cut again with `select=gte(t,T)`
   and looked at against the two videos.
5. **A link said WhatsApp and dialled the phone.** The line under the hero button now reads "Or call +91 76691 40719"
   and is a `tel:` link, so the label and the link agree.
6. **The form threw a ReferenceError when the GSAP CDN was blocked**, because the submit handler called GSAP before the
   GSAP guard. The call is guarded now, and the form was checked with the CDN blocked: the message shows, no errors.
7. **"NMC registered" was not a safe label** - she may be registered with the State Medical Council. It now reads
   "Registered medical practitioner (NMC / State Medical Council)", and the number sits in the `CLINIC` config object
   (`regNumber`) so it is one edit when she sends it.
8. **The companion was hidden from screen readers but still clickable.** It is a labelled link now, and its bubble is
   marked as a status message.
9. **The line under the location cards started with a full stop on a new line** on a phone, because the paragraph was a
   flex row. It is ordinary text again.
10. **The "SUPPORT, NOT A CURE" tag sat on top of the sun character** on the wide multiple-sclerosis card from 620px up.
    The rule that moves that tag back into the text flow was written before the rule that pins it to the corner, and
    they have the same weight, so the corner rule won. The tag now has the higher specificity and the card reads as
    tag, heading, copy, with the character on the right.

Checked again after the fixes: no JavaScript errors at 390x844 or 1440x900, no broken anchors, no duplicate ids, no
horizontal scroll at either width, and the name, the degrees and the booking buttons are all there in the header, in the
credentials band and in the footer. The full-page screenshots are taken after a scroll through the page, because the
sections that rise in on scroll would otherwise be captured empty.

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


### Option 10 - Soft 3D (writer's own check, 13 November 2026)

The first pass of option 10 already had the structure, the copy and the first 3D renders. The pass below is what was
found by actually looking at the page and the recordings, and fixed before the final screenshots were taken.

1. **Every condition tile had lost its text.** `.tile-art` is a `<span>`, and a `<span>` is an inline box, so the
   `width`/`height` on it did nothing: the image inside was 100% of the tile and pushed the description and the
   tag out of the card, which had `overflow:hidden`. On a phone only the heading survived. The art is now a block box
   and the tile is a flex column.
2. **Two headings were invisible on the dark band.** `.evidence-card b` was `var(--ink)` - near-black on a
   near-black card, so "For pain" and "On safety" could not be read. The dark band now sets its own colours.
3. **The companion's halo looked like a scratch on the lens.** In the first render the halo was a hair-thin white
   torus floating above the head, and the crop cut its top, so it read as a stray hair. It is now a thick ring that
   sits on the head, like the Bevel orb in `research/mobbin/ios-bevel-orb-character-checkin.webp`, and the crop box is
   measured on the raw render (every pixel that is not the flat key colour) instead of on the keyed image, so a thin
   bright edge can never be cut off.
4. **The first-visit scene was a white slab.** The table-top scene was built on a cream lathe that filled the bottom
   half of the frame. It is now a soft lilac round mat, and the companion's halo in that scene was hidden behind its
   head, so it was raised and opened out.
5. **The hero was an empty box for the first half second.** The intro faded the headline, the lede and the buttons in
   from `opacity:0`, so the page painted empty and the largest element was not painted until the animation had run.
   The text is now painted on the first frame and only moves with a transform. Measured after the change on a
   throttled phone (Slow 4G, 4x CPU): **LCP 0.95 s, CLS 0.000, FCP 0.48 s**.
6. **The first motion recording caught an empty hero.** `opt10-motion-390-f0s.png` showed nothing but the header and
   the sticky bar, because the recording started a fraction before the intro began. The page now writes
   `window.__introT` so the recorder can time the still frames, and the intro starts with the first paint.
7. **The brand wrapped to two lines on a 390px phone**, because the header button and the brand together were wider
   than the row. The button and the brand are now a little smaller below 480px.
8. **The scrub frames had no camera travel on a phone.** The scene now jumps to the frame of the step you are on,
   the progress bar fills as you scroll, and the label says which step you are on.
9. **Three tiles did not read.** The migraine tile was a plain egg (its ring was hidden behind the orb), the joint
   tile was two balls with a "sausage" behind them, and the certificate was a lavender blob. They are now an orb
   inside two visible rings, a bent joint between two bone ends, and a rolled scroll with a paper and a gold seal.
10. **The video loop could not be used on the page.** ffmpeg on this server cannot mux a VP9 alpha channel into WebM
    (the muxer does not write the alpha flag, and Chrome then paints the video opaque), and an animated WebP of the
    same 6 second loop came out at 2.5 MB. The hero therefore uses the still plus a CSS float, and the 6 second WebM
    (224 KB) ships as the loop export. The real 3D motion on the page is the 24 frame scroll-scrubbed scene.

Checked and needing no change: no horizontal scroll at 390px or 1440px (`scrollWidth - clientWidth = 0`), one
`<h1>`, headings in order (h1 to h4), every word in the HTML, the page reads completely with JavaScript switched
off, `prefers-reduced-motion: reduce` holds every animation still and keeps every picture in place, the WhatsApp
and phone links are all built from the one `CLINIC` object, and there is no cure claim, no price, no testimonial and
no photograph of her anywhere on the page.


### Notes for the next reviewer

- The speed numbers come from a local file or a local HTTP server (`python3 -m http.server`), not from GitHub Pages.
  Real hosting adds TLS and CDN time, so treat the fastest number as a floor, not a promise.
- The `size-adjust` fallback ratios were measured against Arial and Georgia on macOS. On Windows and Android the
  fallback family falls back to the same local fonts (Arial, Liberation Sans, Georgia, Times New Roman), which have
  near-identical metrics, but it is worth one check on a Windows machine.
- Option 9's scene is a fixed layer, so on a short screen the text cards can cover the walker for a few seconds while a
  long card is on screen. The walker always has the left third of the desktop layout to itself; on a phone it is the
  lower part of the screen, under the card.
- The registration number on every page is still a placeholder ("NMC registered - Registration number to be added"),
  and the form on every page is a demo that sends nothing.
