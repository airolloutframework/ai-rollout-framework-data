# Changelog

Dated log of major site and content updates. Backfilled from real
commit history — not a list of every commit, but the milestones that
changed what the site says, how it's structured, or how discoverable
it is.

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
