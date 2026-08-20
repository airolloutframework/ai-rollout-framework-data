# Pricing & Tiers

> **⚠️ High drift risk.** Pricing is the fastest-changing fact on this
> site. The figures below were verified directly against the live site
> (`api/framework.json`, `framework.html`, `employee-training.html`) on
> 2026-08-20 — not retyped from memory. **Include this file in any
> future pricing-consistency audit sweep**, alongside the HTML pages
> and `api/framework.json`.

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
published for this tier on the live site (only the $99 framework has a
stated 30-day guarantee) — do not imply one exists here.

## What each tier is for

The two products are complementary, not competing:

- **The AI Capability Rollout Framework ($99)** is for the manager or
  director leading organization-wide AI adoption — governance, pilots,
  and measurement.
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
bundle). If the embedded Stripe session fails to initialize, a hosted-
checkout fallback is used automatically — both paths route through
`airolloutframework.com`, never a third-party domain.

## Verification checklist for future audits

- [ ] `$99` and `$24.99` figures match across: `api/framework.json`,
      `framework.html`, `employee-training.html`, `index.html`,
      `llms.txt`, `llms-full.txt`
- [ ] `/enroll` and `/enroll?product=team-training` both resolve and
      route to the correct product
- [ ] No stray reference to a third-party checkout domain (Gumroad,
      aibeginner.net, etc.)
- [ ] Money-back guarantee language is only claimed for the $99
      framework tier
