# Changelog

Dated log of major site and content updates. Backfilled from real
commit history — not a list of every commit, but the milestones that
changed what the site says, how it's structured, or how discoverable
it is.

## 2026-10-08

- Social sharing: a default 1200×630 share image (`/images/og-default.jpg`) is now set as og:image and twitter:image on 38 indexable pages, and og:site_name is "AI Rollout Framework" on every page.
- Hardening: Stripe webhook grants access only for paid sessions (and handles delayed-payment events), baseline security headers added site-wide, muted-text contrast raised to WCAG AA.

## 2026-10-07

- New resource page explains EU AI Act Article 4 (AI literacy) and what records to keep; general information, not legal advice.
- New resource page maps the NIST AI RMF's four functions to the 90-day system; FAQs now say "Controlled Pilot" to match /framework.
- AI at Work page now states acceptable-use training, seat page and certificate ID; schema disambiguation added.
- Markdown variants are now generated: `tools/build-md.py` renders each
  page's visible <main> as Markdown (frontmatter, full-URL links, every FAQ
  question and answer) and `--check` reports drift. All 39 .md files were
  regenerated; every indexable page now advertises its .md with a
  `<link rel="alternate" type="text/markdown">` in the head. `npm run check`
  runs the generator check with the other verify scripts. The framework
  page's empty "course outline" box (no button) was removed; the AI at
  Work page shows a worked seat-price example; the homepage transcript
  links its caption and transcript files.
- Paid Framework deliverables are now served only to signed-in members.

## 2026-10-06

- Homepage: a new 2:22 overview video, "The AI Rollout Framework in Two
  Minutes", now sits in the hero under the buttons (Azure `airollout-media`,
  captions off by default with a CC toggle, full transcript on the page,
  its own VideoObject). Directly under it, a two-card "Your next step"
  strip: the free AI Readiness Assessment, then the Executive Suite. The
  three Start-here cards are gone from the hero, and the 2:49 Lesson 1
  preview moved, unchanged, into the framework section.
- The captions toggle is now one shared helper in `js/site.js` (styles in
  `css/site.css`), used by the homepage and the AI at Work player, with the
  same remembered choice across the site.
- AI at Work seat tiers moved to $39 for 1 to 14 seats, $29 for 15 to 49
  and $19 for 50 or more, still applied to the whole order (1 to 500
  seats per order). Co-branding ($249 once) is now free from 50 seats.
  The seat prices themselves are unchanged.
- Every Executive Suite now includes one AI at Work seat, assigned to the
  buyer, for new purchases, the $200 upgrade and the Rollout Pack.
  Existing Suite owners receive it too. Later seat purchases by the same
  email add to the same organization and keep the same enrollment link.
- The Rollout Pack ($899) is now described as the upgrade path for
  Executive Suite buyers: the Suite plus 25 additional seats, 26 in all
  including the seat the Suite already includes ($600 more than the
  Suite; saves $125 versus buying separately).
- Two new Executive Suite files: the AI Glossary for Leaders (20-page
  PDF, ten topic areas, A to Z index) and Leading Our AI Rollout (15
  editable PowerPoint slides with speaker notes).
- The community moved to Discord. `/community/` is now its landing page;
  the earlier on-site discussion forum was retired and its URLs redirect
  there. The $99 framework now lists access to the members-only AI
  Rollout Framework channel; Executive Suite owners get both
  members-only channels.
- The MCP server is version 1.0.2: `get_framework_overview` now carries
  the community and the full Executive Suite contents, and tool
  descriptions read their prices from `api/framework.json`.

## 2026-10-04

- Launched [AI at Work: Essentials for Every Employee](https://airolloutframework.com/employee-training),
  a 49-minute AI training course for every employee: seven modules, 10
  downloads, a 12-question quiz, a completion certificate, two
  interactive tools (Prompt Builder and Time Savings Tracker), and
  optional captions and transcripts. Seats are $39 (1 to 24), $29 (25
  to 99) or $19 (100 or more), with the tier rate applied to the whole
  order; co-branding is $249 once, free at 100+ seats; the Rollout Pack
  (Executive Suite plus 25 seats) is $899. 30-day money-back guarantee.
  Module 1, its transcript and its worksheet are free with no email
  gate.
- Buyers get a seat page (enrollment link, allowed email domains,
  employee progress and CSV export); employees get progress tracking,
  a server-graded quiz and a downloadable certificate. Course videos
  stream from a private container through short-lived signed links.
- Retired The Complete AI Learning Path. Its checkout link now
  redirects to `/employee-training`; the "Team
  Training" nav item is now "AI at Work". `api/framework.json`,
  `api/faq.json`, `llms.txt`, `llms-full.txt`, the docs and the MCP
  server (`get_pricing`, plus a new public `get_ai_at_work_course`
  tool) carry the new course.

## 2026-09-30

- Made the Framework + Executive Suite bundle the lead offer at $299
  (upgrade for framework buyers: $200); the AI Capability Rollout
  Framework on its own stays available at $99 as the lighter option.
  The 30-day guarantee is unchanged. `/enroll` now defaults to the
  Suite with a "Framework only" switch, the home page, `/framework`,
  `/executive`, `/ai-readiness-score` and the sample results page lead
  with the Suite, and every page gains an "Executive Suite" nav item.
  `api/framework.json`, `llms.txt`, `llms-full.txt`, the FAQ, the docs
  and the MCP server's `get_pricing` (now with a `recommendedOffer`
  field) carry the new order and prices.
- Published a two-page
  [Executive Suite overview brochure](https://airolloutframework.com/executive-suite-overview.pdf),
  generated from `api/framework.json` so its prices and contents can't
  drift from the site.

- Published two answer-first governance guides that link to the new
  kit:
  [Why Your Organization Should Use Business or Enterprise AI Plans](https://airolloutframework.com/resources/business-enterprise-ai-plans/)
  (consumer vs. business vs. enterprise plans, with a ChatGPT / Claude /
  Microsoft Copilot / Gemini comparison verified against vendor
  documentation) and
  [Microsoft Copilot Readiness: Fix Oversharing Before You Turn It On](https://airolloutframework.com/resources/microsoft-copilot-readiness/)
  (find, contain, fix and keep-clean steps with Microsoft Purview and
  SharePoint Advanced Management; Restricted SharePoint Search
  retirement). Seven FAQ pairs each with FAQPage schema, Markdown twins,
  and entries in `llms.txt`, `llms-full.txt`, `sitemap.xml`, `rss.xml`,
  the resources hub and [qa-dataset.json](qa-dataset.json).
- Added the Rollout & Operations Kit to the Executive Suite: nine gated
  templates for running an AI rollout day to day — AI Data
  Classification Guide, Enterprise AI Tier Guide, Shadow AI Inventory
  Worksheet, AI Policy Rollout Kit, AI Incident Response Playbook,
  Microsoft Copilot Readiness Guide, Vendor AI Risk Questionnaire, AI
  Champions Program Guide and AI Adoption Scorecard (eight Word
  templates and an Excel spreadsheet). They reuse the AI Governance &
  Policy Kit's data classes, tool tiers and risk ratings. Vendor and
  Microsoft details are stamped "Verified as of 30 September 2026".
- Prices unchanged ($199 bundle, $100 upgrade). Existing Executive
  Suite owners receive the kit at no extra cost.
- Updated the offer description in
  [pricing-and-tiers.md](pricing-and-tiers.md), `api/framework.json`
  (and so the MCP `get_pricing` and `get_framework_overview` output),
  `api/faq.json`, [faq-troubleshooting.md](faq-troubleshooting.md), the
  `/executive` page (new Rollout & Operations Kit section, Product
  schema, FAQ), checkout, the framework and home page cards, `llms.txt`
  and `llms-full.txt`. The files themselves are served only to signed-in
  Executive Suite members.

## 2026-09-29

- Published [Why Do Most AI Pilots Stall?](https://airolloutframework.com/why-ai-pilots-stall),
  the companion article for AI Rollout Podcast Season 3, Episode 11 and
  the first episode in the citation-first format (question-titled
  chapters, answer-first). The page carries the episode itself: YouTube
  player with chapter links, Spotify link, full transcript, and
  `PodcastEpisode` + `VideoObject` schema with one `Clip` per chapter.
  Ten FAQ pairs, a one-page AI pilot charter, and cross-links to and
  from the pilot program guide, the pilot scaling guide, the AI adoption
  framework and the AI implementation roadmap.
- Added "AI pilot charter" and "AI pilot purgatory" to
  [entity-definitions.md](entity-definitions.md) and to the MCP
  `search_knowledge_base` index.
- Added the pilot charter and the pre-mortem to Phase 2 in
  [framework-methodology.md](framework-methodology.md).

## 2026-09-25

- Released the Executive Audio Masterclass (59 minutes, 11 chaptered
  segments) as a gated Executive Suite download: M4A with chapter markers
  plus an MP3 fallback, served from Blob storage after the members
  session check. Sales copy, `api/framework.json`, `api/faq.json`,
  `llms.txt` and `llms-full.txt` now describe it as included rather than
  upcoming.

## 2026-09-23

- Added the Executive Suite: a $199 Framework + Executive Suite bundle
  and a $100 upgrade for existing framework owners, with a new
  `/executive` page (FAQPage schema written around the AI policy
  template searches that DataForSEO showed real, low-difficulty demand
  for). Pricing added to `api/framework.json`, `api/faq.json`, the MCP
  `get_pricing` tool, `llms.txt` and `llms-full.txt`.
- Paid Executive Suite files are served by a session-checked function
  from outside the public site, not from `/course-files/`.

## 2026-09-14 (later)

- Published three long-tail resource pages, each chosen from DataForSEO
  difficulty and volume rather than guesswork: `/resources/ai-adoption-challenges/`
  (KD 5), `/resources/ai-adoption-curve/` (KD 17), and
  `/resources/ai-adoption-strategy/` (KD 24).
- The strategy page states the strategy/framework/roadmap distinction
  explicitly, because `/ai-adoption-framework` and `/ai-implementation-roadmap`
  already hold the neighbouring terms and the three would otherwise compete
  for the same queries.
- `/resources/ai-rollout-framework-guide/` already carried a "Common AI
  adoption challenges" section, so it now defers to the dedicated page rather
  than splitting the phrase between two URLs.

## 2026-09-14

- Added the public Microsoft Learn transcript as verifiable evidence for
  the Microsoft certifications: `learn.microsoft.com/users/azuresteven` in
  Steve Buckner's Person `sameAs`, `recognizedBy` (issuer) on every
  credential, and a transcript `url` on the Microsoft ones. Named-but-
  unlinked credentials are claims; a resolvable transcript is evidence.
- Wired up IndexNow (key file at the site root plus `tools/indexnow.mjs`)
  so a changed page reaches Bing in minutes rather than on crawl schedule.
- Fixed `MAILERLITE_GROUP_TEAM_TRAINING_PURCHASED`, which was missing a
  leading digit — team-training purchasers were never being tagged.
- Forwarded the branded-training interest form to MailerLite; it was the
  one capture point still posting only to Netlify Forms.

## 2026-08-20

- Built `/ai-implementation-roadmap` — a new page targeting "AI
  implementation roadmap," with the real 90-day/three-phase structure,
  Article + HowTo + FAQPage schema, and reciprocal internal linking
  with `/ai-readiness-score`.
- Added YouTube (`@AIRolloutFramework`) as the 10th entry in the
  Organization `sameAs` array, identical across all pages carrying
  Organization schema.
- Renamed the GitHub account from `aibeginnergit` to
  `airolloutframework`; updated the local git remote and repo
  references.
- Populated the Organization `sameAs` array with 9 external entity
  profiles (Product Hunt, Crunchbase, LinkedIn company page, Indie
  Hackers, Spotify, Apple Podcasts, AlternativeTo, SaaSHub, GitHub) and
  added Steve Buckner's personal LinkedIn to his Person schema node.

## 2026-08-19

- Deepened `/ai-readiness-score` for AI-Overview citation: added a
  "built for mid-market teams, not enterprise IT" section, a readiness-
  vs-maturity-model distinction, and 3 new FAQ entries sourced from
  live "People Also Ask" data.
- Scrubbed a legacy "AI Beginner" brand reference from the podcast RSS
  feed (52 episodes) — remapped stale links, fixed a malformed anchor,
  removed invisible characters.
- Sitewide title-length pass: tightened 15 pages from 75–124 characters
  down to 39–50, then a follow-up pass brought the remaining 6
  borderline pages under 60 characters — every indexable page on the
  site is now under the 60-character SERP display limit.
- Refreshed `sitemap.xml` `lastmod` values to real per-page dates.
- Added a standalone-training disclosure to the $24.99 course area,
  clarifying that the four Learning Path courses do not tie into the
  90-day framework.

## 2026-08-18

- Framework free preview switched to the real welcome video (01.mp4);
  reduced checkout friction by moving the Learning Path preview to the
  marketing site.

## 2026-08-17

- Learning Path course area completed: all four courses (Using AI
  Confidently, AI Made Simple, AI Skills Accelerator, AI for Business)
  plus Additional Resources.
- Fixed a Stripe webhook bug mislabeling coupon/Payment-Link purchases
  as the framework product; made the post-purchase `/thank-you` page
  product-specific.

## 2026-08-16

- Course delivery infrastructure built: signed members-area sessions,
  gated video delivery, and supporting tools.

## 2026-08-15

- Fixed AI Readiness Score report downloads to generate personalized
  PDFs client-side.

## Earlier

- Initial site build: ported and rebranded from the prior Blair
  Technology Services structure, with on-domain Stripe checkout, a
  members area, free preview flow, and the SEO/AEO layer (schema,
  `llms.txt`, `robots.txt`, markdown-per-page) in place from launch.
