# Changelog

Dated log of major site and content updates. Backfilled from real
commit history — not a list of every commit, but the milestones that
changed what the site says, how it's structured, or how discoverable
it is.

## 2026-09-30

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
