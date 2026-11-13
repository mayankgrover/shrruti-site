# Homepage design options - Dr. Shruti Grover

Prepared 13 November 2026 for Mayank, to pick one direction for the clinic homepage.

- `index.html` - chooser page with the four options.
- `1/index.html` ... `4/index.html` - the four homepages. Each one is a single self-contained file: inline CSS, Google Fonts, no framework, no build step, relative links only.
- `shots/` - full-page screenshots at 1440px and 390px, plus `opt*-390-top.png` (first phone screen, with the sticky bar in place).

All four pages carry the same facts, in the same order: header, hero, her story (MS), conditions treated, how a first visit works, credentials, location, FAQ (4), booking (WhatsApp + form), footer, sticky "Book on WhatsApp" bar on mobile.

## How to review

1. Open `index.html` in a browser (or serve the folder: `python3 -m http.server`).
2. Open each option on a phone (390px) and a laptop (1440px). The screenshots in `shots/` are the same thing.
3. Pick one, or say "option 2 but with option 3's colours". Mixed directions are normal and cheap to do.
4. Note anything that reads wrong for a family in Delhi/NCR: language, tone, how much is on the page.

---

## 1. The real sites I looked at, and what makes them look premium

All read on **13 November 2026** from the live sites.

| Site | URL | What it does well |
|---|---|---|
| Herb + Ohm (Chicago acupuncture) | https://herbandohm.com/ | One big statement per section ("ANCIENT WISDOM. MODERN CHICAGO."), Montserrat at heavy weights, a clear "book online." button, and 74 images all lazy-loaded so the page stays fast. |
| Resilient Acupuncture | https://resilientacupuncture.com/ | Quiet and editorial: a serif (Old Standard TT) with a handwritten accent face, only 9 images, and the nav is a short list of services. Less is the point. |
| Pacific Bridge Wellness | https://pacificbridgewellness.com/ | The H1 does the selling: "Bridging the East with the West..." - the patient promise is in the first line, not in a slogan. Crimson Text throughout, so the page reads like a book. |
| The Yinova Center | https://yinovacenter.com/ | Cream `#fdf7f2` with deep indigo `#100b36` and a custom serif. Their line "We work in partnership with our patients by carefully tailoring treatments to the individual" is a patient-first promise in plain words. |
| Modern Acupuncture | https://modernacupuncture.com/ | Condition-led navigation (Pain Relief, Sleep, Stress, Fertility...). Deep plum `#381f28` as one confident colour, 29 images all lazy-loaded. |
| Weill Cornell Integrative Medicine | https://weillcornell.org/integrative-health-program | The institutional version: plain explanatory headings, no selling words, a clean definition list, and the institution's own blue/green (`#007bc2`, `#1b7638`) used only for links and rules. Trust comes from structure, not adjectives. |
| Parsley Health | https://www.parsleyhealth.com/ | Premium functional-membership positioning: the offer is stated once, clearly, and the page never shouts. |
| Summit Health | https://www.summithealth.com/ | Multispecialty clinical: strong information hierarchy, so a worried first-time visitor can find the department, the doctors and the phone number fast. |

**What the pattern is (and what I used):**

1. One real promise in the first line, said in plain words - not a slogan. (Pacific Bridge, Yinova)
2. One colour doing the work, plus ink and paper. (Yinova, Modern Acupuncture)
3. A book button that is visible without scrolling on a phone. (Herb + Ohm)
4. Serif for the human story, sans for the practical parts - the page changes register on purpose. (Resilient, Pacific Bridge)
5. Photos that show the room or the practice, not stock smiling faces. (all of them)
6. Lazy-loading on every image below the fold. (Herb + Ohm, Modern Acupuncture)

---

## 2. The four options

### Option 1 - Clinical calm (`1/index.html`)

- **Idea:** white, one deep teal, crisp sans serif, a lot of air. The trust of a hospital with the warmth of a clinic. The credentials strip under the hero is the quiet authority device.
- **Fonts:** Inter (400/500/600/700) only.
- **Colours:** ink `#10242B`, teal `#0E5A63` (hover `#0A434A`), mist `#EEF4F4`, line `#D8E3E3`, WhatsApp green `#106B3B`. Every text/background pair used is at least 4.5:1.
- **Layout:** 2-column hero with the photo on the right and a small clinic card on it; hairline-ruled cards for conditions; steps with a 3px teal rule; location in two bordered panels; FAQ as native `details`; dark footer.
- **Inspired by:** Weill Cornell (structure, plain explanatory headings), Summit Health (fast paths to phone and department), Herb + Ohm (one clear book button), Modern Acupuncture (condition list).
- **Watch out:** it can read a little cold for someone who wants to feel cared for.

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

### Option 4 - Doctor-first authority (`4/index.html`)

- **Idea:** navy and gold, very structured. Her photo slot, her qualifications and the clinic details come before the story. Feels like a private specialist practice.
- **Fonts:** Source Serif 4 (400/600/700) for headings and the credentials table, Inter for body and UI.
- **Colours:** navy `#0B2545` (deep `#071A33`), gold `#B08D4F` (light `#D8BD8B`), ivory `#FAF7F1`, ink `#1A1A1A`, muted `#5A5F6A`, line `#E3DCCE`.
- **Layout:** navy header with a gold rule; hero split with a gold-framed photo placeholder on the left and a quick-facts list (clinic, address, hospital hours, booking, language) on the right; numbered sections (01-07) with gold rules; qualifications as a real table with a caption; location in navy-bordered panels; navy booking band with the form on white.
- **Inspired by:** Summit Health (information hierarchy), Weill Cornell (credentials first, institutional restraint), modern private-practice sites (navy + gold).
- **Watch out:** it is the least warm of the four, and it needs her photograph to work. See the note below on using her photo.

---

## 3. Medical and NMC compliance (why some things are deliberately missing)

Source for the rules below: **National Medical Commission, "Guidelines on Ethical Advertising and Public Communication by hospitals/medical institutions and Registered Medical Practitioners", R-13014/01/2024-Ethics**, https://nmc.org.in/whats-new/download/1874 (read 13 November 2026). Page numbers below are from that PDF.

- **No testimonials, no star ratings.** Explanation V (p.4): an RMP shall not solicit, buy, publish or share patient reviews, ratings, testimonials, endorsements or recommendations for professional promotion. So the "5.0 from 14 reviews" on the Google listing is **not** on the site. This also rules out review widgets and testimonial sections in later pages.
- **No superiority or outcome claims.** Guideline 8.1(iii) (p.8) bans "Guaranteed cures", "Best doctors", "No.1 Specialist", "100% success", "painless treatment", "Miracle treatment". Guideline 8.1(ix) bans "best", "No.1", "leading", "most trusted", "top", "number one", "unmatched". None of these words appear on any of the four pages.
- **No case studies or before/after.** Guideline 8.1(v) (p.8).
- **No prices and no offers.** The brief decides no prices on the site, and Guideline 8.1(x) (p.8) bans free procedures, discounts and anything likely to encourage unnecessary consultation.
- **Full name and qualifications on every page.** Explanation III (p.4): an RMP publishing electronic-media content should disclose name, qualifications, registration status and SMR/NMR registration number. Each page footer carries the name, all three qualifications and a line for the registration number (**to be added - Mayank or Dr. Grover**).
- **Her own photograph.** Guideline 9.2 (p.10): use of the photograph of an RMP shall not be permitted where it constitutes self-advertisement, solicitation or promotional publicity. That is why option 4 shows a clearly marked placeholder and no stock person is presented as her. Decide with Dr. Grover (and, if needed, a lawyer) before any photo of her goes on the site. Guideline 7.2(b) also forbids creating a synthetic person, image or endorsement.
- **Patient privacy.** Guideline 6.1 and 6.2 (p.6): patient photographs, treatment details, testimonials and before/after pictures cannot be used in advertising, and consent does not make them allowed. So: stock photos only, captioned "not a patient", and no patient story on the homepage.
- **AI content.** Guideline 7.2(a) (p.6): AI-generated or AI-assisted content must not be used to create misleading or unverifiable representations about diagnosis, treatment, outcomes, qualifications or patient experience. Every medical line on these pages is either a fact from the brief or carries its source on the page (MS Trust).
- **Medical review date.** Each footer says "Medical content reviewed by Dr. Shruti Grover - Last updated 13 November 2026". That date is a placeholder until Dr. Grover has actually read the page; it must be re-set whenever the copy changes.

### The MS wording (the one claim that needed care)

Every page says acupuncture for MS is **support**, never a cure, and names the limits of the evidence. Source: **Multiple Sclerosis Trust, "Acupuncture" (A-Z of MS)**, last updated 1 April 2022, https://www.mstrust.org.uk/a-z/acupuncture (read 13 November 2026), which says:

- "Acupuncture is a complementary therapy sometimes used by people with multiple sclerosis."
- "Despite some promising results, there's not enough evidence to make claims for or against the use of acupuncture in MS... However, it is generally considered safe when provided by an experienced, trained practitioner using sterile single-use needles."
- A 2014 review of 12 studies suggested possible improvement in quality of life, fatigue, spasticity and pain, "but the poor study designs made it difficult to draw any firm conclusions".
- A 2021 review found traditional and scalp acupuncture "appeared to help improve symptoms including fatigue, pain, walking difficulties and bladder problems".
- A 2018 review found "there wasn't enough evidence that acupuncture (including electroacupuncture) could reduce spasticity in MS".

So the pages promise comfort and quality of life, tell the patient to keep their neurologist, and put the source in front of them.

---

## 4. One config place (so a move is cheap)

The brief says a location change must be cheap. Each page has a single `CLINIC` object at the bottom of the file - address, plus code, phone, WhatsApp link, map link, hospital and hours - and the page fills those spots from it (`data-clinic`, `data-wa`, `data-tel`, `data-maps`).

In the real build (Astro on GitHub Pages) this object becomes one file, `src/data/clinic.json`, rendered at build time, so crawlers and humans read the same values and there is still only one place to edit. The `noscript` block in the location section keeps the address readable if JavaScript is off.

---

## 5. Accessibility, performance and how it was checked

Checked with headless Chrome (Playwright) on 13 November 2026, at 1440px, 390px and 375px:

- No horizontal scroll at 375px, 390px or 1440px on any of the four pages (`scrollWidth - clientWidth = 0`).
- One `<h1>` per page; `header`, `nav`, `main`, `footer` landmarks; a skip link to `#main`.
- Every image has an `alt` that describes what is in the picture; below-the-fold images use `loading="lazy"`, the hero image uses `fetchpriority="high"` and `width`/`height` so nothing jumps while loading.
- Form: three labelled fields (`name`, `phone`, `concern`), `autocomplete` set, and a live region for the demo reply.
- FAQ uses native `details`/`summary`, so it works without JavaScript and can be indexed.
- Focus rings on links, buttons, inputs, textareas and `summary`.
- Contrast: every text/background pair on the four pages is 4.5:1 or better (measured, not guessed).
- Images are hot-linked from `images.unsplash.com` with `auto=format&fit=crop&w=...&q=70`; no image is larger than about 1600px wide.
- All links inside the four pages are relative, so they work from a GitHub Pages sub-path.

Screenshots were taken with headless Chrome (Playwright driving the installed Google Chrome), 1440x900 and 390x844, full page. The equivalent plain-Chrome command for a single viewport is:

```
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new \
  --screenshot=shots/opt1-1440.png --window-size=1440,900 \
  "file://$PWD/website/design-options/1/index.html"
```

For the 390px full-page shots, the sticky bar was pinned to the end of the page for the capture; `opt*-390-top.png` shows it in its real fixed position.

---

## 6. Before this goes live

- Mayank: buy the domain (Decision in the brief), then set `CLINIC` / `clinic.json` once.
- Mayank: get the NMC registration number into the footer of every page.
- Dr. Grover: read the medical copy and set the real medical-review date.
- Dr. Grover + Mayank: decide the her-photo question (NMC Guideline 9.2) before option 4 or any future page uses a photo of her.
- Replace the stock photos with photos of the actual clinic (nobody shows a patient).
- Decide on the form destination (WhatsApp deep link, a form service, or a Google Form for now).
- Add `Physician` / `MedicalClinic` / `FAQPage` schema from the same config file in the real build.

---

## Review notes

_(empty - reviewers and Mayank please write here)_
