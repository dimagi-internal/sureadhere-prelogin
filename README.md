# SureAdhere pre-login website

The public marketing site for **SureAdhere by Dimagi**. It is a static HTML site: no framework, no build step, no database. You edit HTML and CSS files directly, or have Claude Code do it using the skills below.

This README is the orientation guide. The day-to-day editing rules live in `CLAUDE.md`, which Claude Code loads automatically.

## Status: staging, awaiting handover

This repo is the staging copy. Production hosting, repo home, and deploy pipeline are still to be decided by the SureAdhere team. Open items they need to resolve before launch:

1. **Repo home.** This copy lives at `github.com/dimagi-internal/sureadhere-prelogin`. The team may move it into a SureAdhere-owned org or fold it into an existing main repo.
2. **Production URL.** Working assumption is `sureadhere.com` (already owned; today it 301-redirects to `dimagi.com/sureadhere/`). Confirm and lock in.
3. **Deploy pipeline.** No CI workflow exists in this repo. The team picks the host (GitHub Pages, Vercel/Netlify, the dimagi.com static migration pipeline, etc.) and wires push-to-main auto-deploy.
4. **Cutover housekeeping.** At launch, three things need to happen together: (a) flip every `<link rel="canonical">`, `og:url`, JSON-LD `@id`/`url`, `sitemap.xml`, and `robots.txt` from `dimagi.com/sureadhere/` to the new host (the HTML metadata still uses the old URLs intentionally; do not flip until you cut over); (b) add WordPress 301s from `dimagi.com/sureadhere/*` to the new host; (c) update the App Store and Play Store privacy-policy URL fields to wherever `/privacy-policy/` ends up.
5. **HubSpot contact form.** Embed is wired (portalId `503070`, formId `e20b08b5-de23-42b1-9040-b37acff28623`) but the team should confirm submissions land in a watched inbox.
6. **Legal sign-off.** The two privacy policies (English and Mandarin) carry SureAdhere-specific language. Get Dimagi legal's written sign-off before launch.

## Pages and where they live

| File | Live URL | Notes |
|---|---|---|
| `index.html` | `/sureadhere/` | Homepage |
| `clinical-trials/index.html` | `/sureadhere/clinical-trials/` | Solution page |
| `public-health/index.html` | `/sureadhere/public-health/` | Solution page |
| `behavioral-health/index.html` | `/sureadhere/behavioral-health/` | Solution page |
| `resources/index.html` | `/sureadhere/resources/` | FAQ, timeline, release notes |
| `publications/index.html` | `/sureadhere/publications/` | Shown as "Evidence" in the nav: list of studies |
| `contact/index.html` | `/sureadhere/contact/` | Demo request and contact |
| `privacy-policy/index.html` | `/sureadhere/privacy-policy/` | Legal (sync with Dimagi legal) |
| `privacy-policy-chinese/index.html` | `/sureadhere/privacy-policy-chinese/` | Legal, Chinese |
| `login/index.html` | `/sureadhere/login/` | Bare redirect to the secure app |
| `404.html` | served on not-found | Has nav and footer |

Shared assets: `assets/styles.css` (all shared CSS), `assets/images/` (all images), `assets/favicon.png`.
SEO files: `sitemap.xml`, `robots.txt`.

## Run and preview locally

The site is plain files, so any static server works. The repo is already configured two ways:

- **Claude Code preview** (recommended when working in Claude Code): ask Claude to preview; the config in `.claude/launch.json` serves it on port 3030.
- **Manually:** from this folder run `npx serve -p 3030 .` and open `http://localhost:3030`.

Always view the page you changed plus one other page, to catch header/footer drift.

## Making common changes

| You want to... | Do this |
|---|---|
| Change a nav link, the logo, or anything in the footer | Run the `update-header-footer` skill (ask Claude: "update the header/footer"). It edits every page consistently. |
| Add a whole new page | Run the `add-page` skill. It scaffolds the page and registers it in the sitemap and footer. |
| Add a study to the Evidence page | Run the `add-publication` skill. |
| Edit copy or images on one existing page | Edit that page's HTML directly, following the brand and content rules in `CLAUDE.md`. |
| Change colors, spacing, or shared components | Edit `assets/styles.css`, using the existing CSS variables. |

## Skills (in `.claude/skills/`)
- **update-header-footer**: propagate a nav/footer change to all 10 pages, handling the root-vs-subpage path difference and the active-nav state.
- **add-page**: create a new page from the canonical template and register it everywhere it needs to appear.
- **add-publication**: add a correctly formatted study to the Evidence page.

## SEO files to keep current
- `sitemap.xml` lists every public URL. Update it when you add, remove, or rename a page.
- `robots.txt` currently points the sitemap at `/sitemap.xml`. Update it to the absolute URL if SureAdhere moves to its own domain.
- Each page has its own `<title>`, `<meta name="description">`, canonical URL, and Open Graph (`og:`) tags in its `<head>`. When you clone a page, change all of these; do not leave the source page's metadata in place.

## Brand and assets
- Teal `#0DA89D` primary; Work Sans and JetBrains Mono fonts.
- Logo: `assets/images/sureadhere-logo-full-color.png` (rendered white via a CSS filter in the nav and footer).
- App store badges: `assets/images/badge-app-store.svg`, `assets/images/badge-google-play.png`.

## Handle with care
- **Legal pages.** The two privacy policies are legal text. Coordinate edits with Dimagi legal.
- **External links.** The "Sign In" button, the login redirect, the help site, and the app store badges point to live systems. Do not change these URLs without confirming the new target.
- **Version control.** This folder is a git repository with its origin at `github.com/dimagi-internal/sureadhere-prelogin` (the staging copy). Commit every change there so the team has history and a safe undo, and run `git push` after committing. Confirm the repo's visibility (public vs private) in its GitHub settings before sharing it widely. The SureAdhere team may relocate this repo to a SureAdhere-owned org at handover.

## Deploy

This repo is staging only — see the "Status" section at the top for the full list of decisions the SureAdhere team needs to make before launch (repo home, production URL, host, cutover housekeeping). Replace this section with the confirmed steps and the list of who can publish once the deploy pipeline is wired.

Today's canonical URLs in the HTML (`<link rel="canonical">`, `og:url`, JSON-LD `@id`/`url`, `sitemap.xml`) all still point to `https://dimagi.com/sureadhere/`. They are intentionally left untouched in this staging state — they should be flipped to the new host as part of the cutover, not before.
