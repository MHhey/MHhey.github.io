# MHhey.github.io

Plain HTML and CSS. No build step, no dependencies.

```
index.html                    single page
beyond.html                   volunteering, honours, outreach
style.css                     design tokens in :root at the top
favicon.svg
projects/
  agentic-bullwhip.html
  document-pipelines.html
  supply-network-study.html
  teaching-robots.html
  housing-platform.html
```

## What this site is for

A supplement to your résumé when applying to construction technology companies. It is deliberately
**not** your CV. Someone at Doxel, Kaya, Krane, DPR or Mortenson has your résumé open in another tab
and 30 seconds here.

The site leads with construction and treats the software as what you bring to it, not the other way
round. Every project card opens with the construction problem in plain language before it names a
framework, so a non-technical recruiter can follow it.

Cut on purpose: the full publication list, peer review record, awards, fellowships, GRE/TOEFL
scores, and the standalone publications page. A handful of papers remain on the homepage, chosen for
relevance to AI and supply chain work, with a Scholar link for the rest.

## Deploy

Repo must be named exactly `MHhey.github.io`, files at the root.

```bash
git add .
git commit -m "update"
git push
```

**Settings → Pages → Source: Deploy from a branch → main / (root)**.

Local preview: `python3 -m http.server 8000`

## Status

Résumé, photo, and placeholder links are in. Demo videos are live on document-pipelines,
housing-platform, and supply-network-study.

**Still open:**
- Buy a domain (~$12/yr), point it at Pages via Settings → Pages → Custom domain
- Double-check your degree titles read the same way across the CV, résumé, and site before sending
  anything out — this was flagged once already as inconsistent

## Adding a project

Copy any file in `projects/`, edit it, add a matching `<article class="card">` in `index.html`, and
fix the `.pager` links on the neighbouring pages.

Page structure: **Overview → how it's built → findings/scenarios → notes → repository.**

## Adding a demo video

Self-hosted, in the project's own folder:

```html
<figure class="media">
  <div class="media-frame">
    <video controls preload="metadata" playsinline muted poster="demo-poster.jpg">
      <source src="demo.mp4" type="video/mp4">
      Your browser does not support embedded video.
      <a href="demo.mp4">Download the walkthrough</a> instead.
    </video>
  </div>
  <figcaption>Caption here.</figcaption>
</figure>
```

GitHub's web uploader caps at 25 MB; pushing via git only caps at 100 MB per file, so push from the
command line for anything larger. Aim for under 20 MB and 60–90 seconds regardless, compressed with
something like:

```bash
ffmpeg -i demo.mp4 -vcodec libx264 -crf 28 -preset slow -vf scale=1280:-2 -an -movflags +faststart demo-web.mp4
ffmpeg -i demo-web.mp4 -ss 00:01:20 -vframes 1 demo-poster.jpg
```

## Design

- Concrete `#E4E4DF`, graphite `#333A3F`, hi-vis amber `#F0B429`, deep teal `#14605C`
- Space Grotesk (display), IBM Plex Sans (body), IBM Plex Mono (labels, data)
- Hero animation: 620 drifting dots on canvas, ~27-second loop, forming construction materials then
  an axonometric building. Renders static under `prefers-reduced-motion`, hidden in print.
- Photo galleries on project pages render greyscale, full colour on hover. Keep photos to their
  natural aspect ratio rather than forcing a shared crop, that's what caused the cropping issues
  earlier, stack them separately instead of in a grid if they don't share a ratio.

### Accessibility and print

- All text passes WCAG AA contrast.
- Nav and hero links have 44px tap targets on mobile.
- `@media print` strips the chrome and expands link URLs, since recruiters save to PDF.

Responsive to 320px, keyboard-navigable, visible focus states.

## Next

- Add a photo or diagram to any project page still running text-only
- Revisit the résumé link once you've settled which of your three résumés matches this site's
  framing
