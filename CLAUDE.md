# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Static site for semlerteaches.com — a high school wood shop teacher's site. No build step, no framework, no dependencies: three hand-written HTML pages with inline CSS, served by GitHub Pages off `main` (custom domain via `CNAME`). Pushing to `main` deploys the live site.

**Site purpose (decided June 2026; expanded July 2026):** three jobs — (1) a student portal (the classroom page), (2) a link-in-bio home base for the owner's social media push as @semlerteaches on TikTok/Instagram/YouTube, and (3) a lead page for **Semler Web Services**, the owner's web-building business (he does NOT own semlerwebservices.com, so it lives here as the `#web-services` homepage section). Selling lesson plans is deferred until he has an audience; don't add storefronts, fake "buy" buttons, or a blog. The Amazon affiliate link stays. He has no videos posted yet — the homepage has honest "first videos coming" copy and should get a featured-video embed once real videos exist.

**Web Services section (`#web-services`):** business email is `semlerwebservices@gmail.com` and the public phone is the **Google Voice number 320.425.0080** — both are live CTAs (the call button `tel:+13204250080` is active). The owner's personal cell **612.363.1999 stays private** — never publish it. A `ProfessionalService` JSON-LD block in `index.html`'s `<head>` backs this section — keep it in sync with the section (towns, pricing, email, `telephone`).

## Commands

```bash
# Preview locally
python3 -m http.server 8741

# Screenshot a page to verify changes (do this before pushing)
google-chrome --headless --disable-gpu --screenshot=/tmp/shot.png \
  --window-size=1280,1800 --hide-scrollbars "http://localhost:8741/index.html"
# Mobile check: use --window-size=390,844
```

## Structure

- `index.html` — link-in-bio style hub: hero banner, big TikTok/IG/YouTube follow buttons, three "door" cards (students / followers / teachers), Reel Log app feature, Amazon support box, social links
- `lesson-plans.html` — short "coming soon" page (no catalog) routing students to the classroom and teachers to follow/email; bring the catalog back only when real TpT/Etsy stores exist
- `classroom.html` — student resources behind a class-code gate (`CODE = "semler"` in inline JS; sessionStorage keeps it unlocked). Resources link to Google Docs.
- `images/` — site images, including `shop-banner.png` (the hero)

Each page duplicates its full CSS and the shared header/nav/footer inline. **There is no shared stylesheet — any change to the palette, nav, or footer must be applied to all three HTML files.**

## Design rules (chosen by the owner — keep this look)

Warm wood-shop rustic, not startup-generic:

- Palette via `:root` vars: bg `#f6f0e4` (cream), text `#2e2014` (walnut), accent `#7a4a10` (wood), `#c9963a` (gold), dark `#2a1400`, borders `#e0d3bc`
- Fonts: Oswald (uppercase headings, `.logo`, buttons) + Source Sans 3 (body), loaded from Google Fonts
- Dark wood headers/footers use a plank texture: `repeating-linear-gradient` lines over a brown gradient; footers have a 6px gold top border
- Corners are 6–8px radius — no pill buttons, no 20px+ rounded cards
- Cards get a 5px wood or gold accent border on one edge
- Avoid the "vibecoded" look: no purple/blue gradients, no new emoji-as-icons, no `border-radius: 999px`

## Hard requirements

- The Amazon affiliate link `https://amzn.to/4e2d30a` (tag `semlerteaches-20`, goes to the Amazon homepage) must keep `rel="sponsored noopener"`, and every page containing it must keep the footer line "As an Amazon Associate I earn from qualifying purchases."
- **Never commit** `Lesson Plans/`, `attachments/`, or `attachments.zip` — they contain the owner's paid lesson plan documents; the repo is public and Pages would publish them.
- The owner sells these plans, so the classroom gate is intentional friction — don't "simplify" it away or move the resource links outside the gate.
