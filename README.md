# MHhey.github.io

Plain HTML and CSS. No build step, no dependencies.

```
index.html                    single page
style.css                     design tokens in :root at the top
favicon.svg
projects/
  agentic-bullwhip.html
  document-pipelines.html     ← demo video slot
  image-classification.html
  housing-platform.html
Heydari-Resume.pdf            ← you add this
```

## What this site is for

A supplement to your résumé when applying to construction technology companies. It is deliberately
**not** your CV. Someone at Doxel, Kaya, Krane, DPR or Mortenson has your résumé open in another tab
and 30 seconds here.

The site leads with construction and treats the software as what you bring to it, not the other way
round. That ordering is the point: at your target companies, engineers who can build are common and
engineers who understand a submittal are rare. Every project card opens with the construction
problem in plain language before it names a framework, so a non-technical recruiter can follow it.

Cut on purpose: the full publication list, peer review record, awards, fellowships, GRE/TOEFL
scores, research interests, and the standalone publications page. Three papers remain, chosen for
relevance to AI and supply chain work, with a Scholar link for anyone who wants the rest. Pre-2023
positions are compressed into one "Earlier" entry.

If you later want a version for academic or research-scientist applications, that's a different
site and should be built as one.

## Deploy

Repo must be named exactly `MHhey.github.io`, files at the root.

```bash
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/MHhey/MHhey.github.io.git
git push -u origin main
```

Then **Settings → Pages → Source: Deploy from a branch → main / (root)**.

Local preview: `python3 -m http.server 8000`

## Before publishing

1. **Placeholder links.** Search for `data-fill` — 3 instances, all `href="#"`. Fill in LinkedIn
   (×2) and Google Scholar (×1), then delete the attribute.
2. **Résumé.** Add `Heydari-Resume.pdf` at the root. Use the CS/AI version — the site is written to
   match that framing, and a construction PM résumé behind this page would read as a mismatch.
3. **Photo.** This is the biggest remaining gap. Add a square photo (~600px) as `photo.jpg` at the
   root, then uncomment the `PORTRAIT` block at the top of `index.html`. It renders greyscale at
   180px beside the intro. Both of the sites you showed me have one; recruiters look.

## Verify

Details I inferred rather than took from your documents. Check before an interviewer asks:

- `agentic-bullwhip.html`: deterministic simulation core, execution loop, repeated seeds, prompt
  versioning
- `image-classification.html`: staged unfreezing, augmentation, 32×32 upsampling
- `housing-platform.html`: the concurrency note

**Your degree titles conflict across your three documents.** The CV says *PhD, Environmental Design
and Planning* / *M.Eng., Computer Science*; your résumés say *Construction Engineering and
Management* / *M.Sc.* The site uses the CV version. Make all of them match before you send anything.

## Demo video

`projects/document-pipelines.html`, comment block marked `DEMO VIDEO`. Replace the
`<div class="pending">` with:

```html
<iframe src="https://www.youtube.com/embed/VIDEO_ID"
        title="Pipeline demo" allowfullscreen loading="lazy"></iframe>
```

or self-hosted (`demo.mp4` in `projects/`):

```html
<video controls preload="metadata" poster="demo-poster.jpg">
  <source src="demo.mp4" type="video/mp4">
</video>
```

Use YouTube unlisted — GitHub Pages caps repos at 1 GB. Clear the content with Intellus first.

## Adding a project

Copy any file in `projects/`, edit it, add a matching `<article class="card">` in `index.html`, and
fix the `.pager` links on the neighbouring pages.

Page structure: **Overview → configuration/stack → implementation (numbered) → notes → repository.**

## Design

- Concrete `#E4E4DF`, graphite `#333A3F`, hi-vis amber `#F0B429`, deep teal `#14605C`
- Space Grotesk (display), IBM Plex Sans (body), IBM Plex Mono (labels, data)
- Hero animation: a Supply / Plan / Build sequence. Material pulses (amber) converge along
  flight-path arcs into a hub, an agent cluster (teal pings) plans while a three-bar schedule fills
  in with the critical path in amber, a signal travels to the site, and a five-level frame rises to
  an amber topping-out beam. Plays once as an ~8-second story on load, then keeps ambient motion
  (pulses, agent pings, beacon). Pure CSS + SVG SMIL, no JavaScript. Under
  `prefers-reduced-motion` everything renders complete and static. Hidden in print.
- The bullwhip wave animation now lives on the bullwhip project page
  (`projects/agentic-bullwhip.html`), with all five tier labels and a technical caption, where the
  surrounding text gives it context. Space is reserved there for your demo video and further
  explanation.

### Accessibility and print

- All text passes WCAG AA contrast. Verified: body 9.1:1, links 5.8:1, dark-band text 5.4–8.2:1,
  amber button 9.7:1.
- Card borders sit at 2.2:1 against the page, below the 3:1 non-text threshold. Deliberate: the
  cards are already identifiable by background, heading link, hover and focus states, and a 3:1
  border would read as a heavy outline. If you'd rather pass strictly, set `--rule-strong` to
  `#7A7A70`.
- Nav and hero links have 44px tap targets on mobile.
- `@media print` at the bottom of `style.css` strips the chrome, expands link URLs and avoids
  breaking cards across pages — recruiters save to PDF.

Responsive to 320px, keyboard-navigable, visible focus states. `style.css` still contains unused
`.split`, `.tally` and `.plain` classes if you want to add a service or volunteering block later.

## Next

- Buy a domain (~$12/yr), point it at Pages via **Settings → Pages → Custom domain**
- Add screenshots or diagrams to the project pages. They are currently all prose, which is the
  weakest thing about them visually. One architecture diagram on the bullwhip page and one output
  screenshot on the housing platform would do more than any amount of extra copy.
