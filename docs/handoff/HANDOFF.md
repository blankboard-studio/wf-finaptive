# Finaptive — design handoff → Webflow build

The brief every build session starts from. Written when the design is
approved (by the designer, or at the end of the prototype phase) and kept
current during the build. Agents read it after `AGENTS.md` and `GOTCHAS.md`.

## Read first

1. `AGENTS.md`, `GOTCHAS.md`, and the skill's `conventions.md`.
2. This file, then `MANUAL-TODO.md` and `BUILD-NOTES.md` in this folder;
   after the build handoff, `REVIEW.md` (feedback rounds until launch) and
   `SEO-PLAN.md`.
3. The approved design: Figma `H1LFhkNHxKV007rnjJCEDn`, page
   "↪ • Case Study Site (Final)" (node `2258:2843`), one column per
   template, desktop 1680 + mobile 375. The prototype (`../prototype`,
   `pnpm dev` → http://127.0.0.1:5966) once pages are approved.

## Status

2026-10-28 — Repo `blankboard-studio/wf-finaptive` created from wf-template
0.8.1 and filled in (`pnpm new-project`); workspace and prototype set up.
Token proposal P1–P10 written in `prototype/src/css/proposed.css` and shown
on the prototype style guide; approved 2026-10-28 with the component plan. No Webflow site yet:
the starter site has to be rebuilt first (MANUAL-TODO A). Next: prototype pages one per session,
starting with Home.

## Ground rules for this project

- Webflow writes only after the person's go-ahead in chat, batch by batch,
  through the project's own MCP server (`webflow-finaptive`).
- Purpose: a portfolio case study rebuild of https://www.finaptive.com/;
  live copy wins over older Figma copy where they differ.
- Design frame 1680, fluid scaling 1440–1680 (template default, no change).

## Pages

| URL | Design source (Figma node, desktop / mobile) | Webflow page | Notes |
| --- | --- | --- | --- |
| `/` | 2258:2846 / 2266:1189 | Home | Industries are tabs here, not pages |
| `/about` | 2258:3520 / 2267:1306 | About | |
| `/contact` | 2258:6522 / 2267:1487 | Contact | form |
| `/careers` | 2258:6640 / 2267:1613 | Careers | lists Jobs |
| `/job/<slug>` | 2261:673 / 2268:1568 | Jobs template | CMS template, 3 items |
| `/solutions/<slug>` | 2258:6741 / 2268:1737 | Solutions template | CMS template, 5 items (open decision 1) |
| `/resources` | 2263:1111 / 2268:1908 | Resources | lists Blog Posts + Events |
| `/blog/<slug>` | 2264:1017 / 2268:2026 | Blog Posts template | CMS template, 5 items |
| `/events/<slug>` | 2258:7311 / 2269:1887 | Events template | Lunch & Learn, 3 items |
| `/event/<slug>` | 2264:4443 / 2269:2061 | Web Sessions template | 3 items (open decision 2) |
| `/scan` | 2258:7513 / 2258:7628 | Clarity Scan | form |
| `/legal/privacy-policy` | 2258:7745 / 2269:2232 | Privacy Policy (folder `legal`) | |
| `/legal/terms-of-service` | 2262:774 / 2269:2305 | Terms of Service (folder `legal`) | |
| `/404` | 2262:928 / 2269:2380 | 404 | |
| `/design/style-guide` | generated | Style guide (folder `design`) | first page built; excluded from search |

Breakpoints: 991 (tablet), 767 (mobile landscape), 479 (mobile). Checked at
1440, 820 and 390. The design has no tablet frames: tablet follows the
desktop layout stacked, decided per page in the prototype.

## Variables and classes

- Variable changes, as old → new, grouped for approval:
  `prototype/src/css/proposed.css` P1–P10 (colours, two font families,
  type roles per breakpoint, layout, radius, Body tag style).
- New classes: none yet (`prototype/CLASSES.md` once pages start).
- Approval state: P1–P10 and the component plan approved by the person in chat, 2026-10-28. Not yet made in Webflow (no site).

## CMS

Proposed from the live site's URLs; fields to confirm (open decision 3).

| Collection | Fields | Used on |
| --- | --- | --- |
| Solutions | Name, Slug, Eyebrow (text), Summary (text), Hero image, Body (rich text), Capabilities (rich text), Order (number) | `/solutions/<slug>`, nav dropdown, Home solutions list (sort: Order) |
| Blog Posts | Name, Slug, Excerpt, Main image, Body (rich text), Author (text), Published (date), Category (option) | `/blog/<slug>`, Resources (newest first) |
| Jobs | Name, Slug, Location (text), Type (option), Summary, Body (rich text), Open (switch) | `/job/<slug>`, Careers list (Open only) |
| Events | Name, Slug, City (option), Date (date), Venue, Summary, Body (rich text), Register URL (link), Image | `/events/<slug>`, Resources, Home (upcoming first) |
| Web Sessions | Name, Slug, Date, Speakers (rich text), Summary, Body (rich text), Register URL, Image | `/event/<slug>`, Resources |

## Components to make

Component plan from the Figma templates, to approve before the first page.

| Component | Used on | Props | Behaviour inside |
| --- | --- | --- | --- |
| Nav (G \| Nav W) | every page | — | Solutions dropdown, mobile menu |
| Footer (G \| Footer W) | every page | — | newsletter form |
| Button | everywhere | Label, Link, Variant (Primary red / Secondary outline / On Dark) | — |
| Page Hero | About, Contact, Careers, Resources, Solutions, legal, 404 | Breadcrumb, Title, Body, Show CTAs, CTA 1/2, Image | — |
| Section Title | most sections | Eyebrow, Heading, Body | — |
| Card | Home, Careers, Resources, Solutions | Tag, Title, Body, Link, Image, Show Tag | — |
| CTA Band | every page above the footer | Heading, Body, Button | — |
| Stat | Home, About | Number, Label | — |
| Event Meta | Events, Web Sessions | Date, Time, Place | — |
| Form Field | Contact, Scan, Footer, events | Label, Placeholder, Required | — |

Page-specific (classes only): Home industry tabs, About timeline/team grid,
Clarity Scan steps, legal page sidebar, blog article body.

## Modules

| Module | `data-*` hooks | What it does |
| --- | --- | --- |
| tabs (Home industries) | `data-tabs`, `data-tab`, `data-tab-panel` | to confirm in the prototype; Webflow Tabs may do |
| mobile menu | `data-menu-toggle` | to confirm; Webflow Navbar may do |

## Decisions

- 2026-10-28 · Repo lives in the `blankboard-studio` GitHub org (public, so
  jsDelivr can serve releases).
- 2026-10-28 · Prototype first; the Webflow starter site doesn't exist any
  more and is rebuilt from `webflow-build/starter-site.md` before the build.
- 2026-10-28 · Fonts from Google Fonts (Inter, Poppins), not uploaded; the
  starter's Geist and its stylistic sets are dropped (P5, P10).

## Open decisions

| Item | Now | Options |
| --- | --- | --- |
| 1. Solutions as CMS or 5 static pages | CMS proposed | CMS template (one design, editable) / static pages |
| 2. `/events/` vs `/event/` | two collections, as live | keep both slugs (case study fidelity) / merge into one Events collection with a Type field and redirects |
| 3. CMS fields | proposed above | confirm against live content |
| 4. Tablet layout | stacked desktop | add tablet frames in Figma / decide in prototype |
| 5. Webflow plan / staging slug | `finaptive` assumed | confirm when the site is created |

## Stand-in assets and placeholders

- Copy written for the case study, to review: Job Detail requirements and
  hiring steps, About team roles, Terms of Service text, 404 links, blog
  pull quote (all in the Figma frames above).
- Images: exported from Figma into `Assets/figma/` as each page is built.
