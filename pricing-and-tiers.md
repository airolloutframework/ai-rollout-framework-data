# Pricing & Tiers

> **⚠️ High drift risk.** Pricing is the fastest-changing fact on this
> site. `api/framework.json` is the source of truth (the MCP server's
> `get_pricing` tool reads it directly); this file mirrors it. The
> framework and Learning Path figures were verified against the live site
> on 2026-08-20; the Executive Suite figures were added from
> `api/framework.json` on 2026-09-23, and the Rollout & Operations Kit
contents on 2026-09-30 (prices unchanged). **Include this file in any future
> pricing-consistency audit sweep**, alongside the HTML pages and
> `api/framework.json`.

## AI Capability Rollout Framework

| | |
|---|---|
| **Price** | $99 USD |
| **Billing** | One-time payment |
| **Access** | Lifetime — all current content and future framework updates |
| **Guarantee** | 30-day money-back guarantee — full refund, no questions asked, if you work through the framework and don't feel it was worth the investment |
| **Checkout** | [airolloutframework.com/enroll](https://airolloutframework.com/enroll) |
| **Landing page** | [airolloutframework.com/framework](https://airolloutframework.com/framework) |
| **Free entry point** | [AI Readiness Score](https://airolloutframework.com/ai-readiness-score) (free, 3–5 min) |

No subscription, no renewal fee, no hidden charges.

## AI Capability Rollout Framework + Executive Suite

| | |
|---|---|
| **Price** | $199 USD |
| **Upgrade price** | $100 USD — existing framework owners only, signed in to the members area |
| **Billing** | One-time payment |
| **Access** | Lifetime — the complete framework plus the Executive Suite, and future Executive Suite additions |
| **Guarantee** | 30-day money-back guarantee — same terms as the framework, on the $199 bundle and the $100 upgrade |
| **Checkout** | [airolloutframework.com/enroll?product=executive](https://airolloutframework.com/enroll?product=executive) (upgrade: `/enroll?product=executive-upgrade`) |
| **Landing page** | [airolloutframework.com/executive](https://airolloutframework.com/executive) |

Includes everything in the $99 framework, plus: the Board Briefing Pack
(editable PowerPoint), the AI ROI & Impact Calculator, the AI Governance
& Policy Kit (three editable Word templates — not legal advice), and
90-day execution roadmaps for Sales, Operations, HR, Marketing and IT
(HR, Marketing and IT added after launch), and the Executive Audio
Masterclass (59 minutes of audio in 11 chaptered segments; M4A with
chapter markers plus an MP3 fallback, released 2026-09-25), and the
Rollout & Operations Kit (added 2026-09-30): nine templates for running
the rollout day to day —

1. **AI Data Classification Guide** — Twelve everyday examples showing
   employees which information can go into which AI tool.
2. **Enterprise AI Tier Guide** — Why company data belongs on business
   and enterprise AI plans, with a platform comparison worksheet and a
   setup checklist.
3. **Shadow AI Inventory Worksheet** — An employee survey, an IT
   discovery checklist and a register for finding the AI tools already
   in use.
4. **AI Policy Rollout Kit** — An announcement email, manager talking
   points, an employee FAQ, a one-page quick reference, an
   acknowledgement log and a refresher schedule.
5. **AI Incident Response Playbook** — First-hour steps, severity
   ratings and containment for five common AI incidents.
6. **Microsoft Copilot Readiness Guide** — A checklist for fixing
   oversharing before you turn on Microsoft Copilot (formerly Microsoft
   365 Copilot).
7. **Vendor AI Risk Questionnaire** — A short questionnaire for software
   vendors that are adding AI features.
8. **AI Champions Program Guide** — How to choose, run and recognise a
   network of department AI champions.
9. **AI Adoption Scorecard** — A spreadsheet tracking licensed and
   active users, policy acknowledgement, training, incidents and
   sentiment, with a check against your ROI assumptions.

Eight editable Word templates and one Excel spreadsheet; templates, not
legal advice. Existing Executive Suite owners receive the kit at no
extra cost, under the "future Executive Suite additions" access term.
Everywhere except `/executive` and this file, the nine are listed as one
item: "Rollout & Operations Kit (nine templates for running the
rollout)", with the topic list in `api/framework.json`.

There is no standalone Executive-only product: it is a bundle upgrade,
not a third tier.

## The Complete AI Learning Path (4-Course Master Bundle)

| | |
|---|---|
| **Price** | $24.99 USD per user |
| **Billing** | One-time payment, per seat |
| **Access** | Lifetime — all four courses |
| **Multi-seat** | Email info@airolloutframework.com with the number of seats for organization pricing |
| **Checkout** | [airolloutframework.com/enroll?product=team-training](https://airolloutframework.com/enroll?product=team-training) |
| **Landing page** | [airolloutframework.com/employee-training](https://airolloutframework.com/employee-training) |
| **Free entry point** | Free sample pack — one preview lesson from each course, a starter PDF, a free audiobook, and the full syllabus |

No subscription, no renewal fee. No money-back guarantee is currently
published for this tier on the live site (only the framework and the
Executive Suite have a stated 30-day guarantee) — do not imply one
exists here.

## What each tier is for

The products are complementary, not competing:

- **The AI Capability Rollout Framework ($99)** is for the manager or
  director leading organization-wide AI adoption — governance, pilots,
  and measurement. It is the complete framework on its own.
- **The Framework + Executive Suite ($199)** is for the leader who also
  has to present the programme upward — to a board or leadership team.
  It adds the investment case, ROI model, AI policy templates and
  department roadmaps.
- **The Complete AI Learning Path ($24.99/user)** is the employee-
  facing companion — practical AI skills training for the people
  actually using AI day to day. It is standalone AI-literacy training
  and does not tie into the 90-day framework's phase structure.

Many organizations use both: the Framework to lead the rollout, the
Learning Path to build team-wide capability.

## Checkout mechanics (for reference, not pricing)

Checkout runs on-domain via Stripe, embedded on `/enroll`. The product
is selected by a `product` query parameter (`/enroll` defaults to the
$99 framework; `/enroll?product=team-training` selects the $24.99
bundle; `/enroll?product=executive` the $199 Executive Suite bundle;
`/enroll?product=executive-upgrade` the $100 upgrade, which the server
only sells to a signed-in framework owner). If the embedded Stripe session fails to initialize, a hosted-
checkout fallback is used automatically — both paths route through
`airolloutframework.com`, never a third-party domain.

## Verification checklist for future audits

- [ ] `$99`, `$199`, `$100` and `$24.99` figures match across:
      `api/framework.json`, `api/faq.json`, `framework.html`,
      `executive.html`, `employee-training.html`, `index.html`,
      `llms.txt`, `llms-full.txt`, and the MCP `get_pricing` output
- [ ] `/enroll`, `/enroll?product=team-training`,
      `/enroll?product=executive` and `/enroll?product=executive-upgrade`
      all resolve and route to the correct product
- [ ] No stray reference to a third-party checkout domain (Gumroad,
      aibeginner.net, etc.)
- [ ] Money-back guarantee language is only claimed for the $99
      framework and the Executive Suite ($199 bundle / $100 upgrade)
- [ ] **Yearly (manual):** `priceValidUntil` on the four Offers
      (`executive.html`, `framework.html`, `index.html`,
      `employee-training.html`) is 2027-12-31. Push it out a year before
      it lapses — an expired date can suppress Google's price snippet.
      Deliberately manual: the site has no build step to roll it.
