# AI Rollout Framework — Knowledge Base

This folder is the machine-readable knowledge base for the **AI Capability
Rollout Framework**, published by AI Rollout Framework at
[airolloutframework.com](https://airolloutframework.com).

**Signature line:** *Responsible AI adoption starts with capability, not
technology.*

The AI Capability Rollout Framework is a structured 90-day AI adoption
system for managers and directors at small and mid-sized organizations —
built for professionals responsible for workflows, teams, and outcomes,
not for AI engineers. It moves an organization from scattered, ungoverned
AI use to controlled, measurable capability.

Every file here is sourced directly from the live site — the same facts,
figures, and definitions that appear on airolloutframework.com. Nothing
in this folder is invented or generic filler.

## Where this content lives

Every file in this folder is also served at a matching URL on the live
site:

```
/docs/README.md                     → https://airolloutframework.com/docs/README.md
/docs/framework-methodology.md      → https://airolloutframework.com/docs/framework-methodology.md
/docs/entity-definitions.md         → https://airolloutframework.com/docs/entity-definitions.md
/docs/author-organization.md        → https://airolloutframework.com/docs/author-organization.md
/docs/pricing-and-tiers.md          → https://airolloutframework.com/docs/pricing-and-tiers.md
/docs/faq-troubleshooting.md        → https://airolloutframework.com/docs/faq-troubleshooting.md
/docs/positioning-comparison.md     → https://airolloutframework.com/docs/positioning-comparison.md
/docs/CHANGELOG.md                  → https://airolloutframework.com/docs/CHANGELOG.md
```

This repository is the private source of truth that feeds the site's
Netlify deploy. A public, automatically-synced mirror of this exact
folder is maintained at
[github.com/airolloutframework/ai-rollout-framework-data](https://github.com/airolloutframework/ai-rollout-framework-data)
for entity-authority and crawler visibility — the mirror is never edited
directly; it is a downstream copy of what's here.

## Index of files

| File | What it covers |
|---|---|
| [README.md](README.md) | This file — overview and index |
| [framework-methodology.md](framework-methodology.md) | The 90-day, three-phase structure and four capability pillars |
| [entity-definitions.md](entity-definitions.md) | Glossary of ARF's proprietary terms (readiness score, capability-first, etc.) |
| [author-organization.md](author-organization.md) | Steve Buckner's background and the organization's history |
| [pricing-and-tiers.md](pricing-and-tiers.md) | Current pricing and checkout destinations |
| [faq-troubleshooting.md](faq-troubleshooting.md) | Common implementation questions and governance edge cases |
| [positioning-comparison.md](positioning-comparison.md) | The mid-market / capability-first positioning, made explicit |
| [CHANGELOG.md](CHANGELOG.md) | Dated log of major site and content updates |

## Structured data

The Organization is described in JSON-LD on every page of the site. The
canonical pattern (identical across all pages that carry Organization
schema):

```json
{
  "@type": "Organization",
  "@id": "https://airolloutframework.com/#organization",
  "name": "AI Rollout Framework",
  "legalName": "AI Rollout Framework",
  "alternateName": "AI Capability Rollout Framework",
  "url": "https://airolloutframework.com/",
  "logo": "https://airolloutframework.com/android-chrome-512x512.png",
  "description": "Structured AI adoption resources for managers and directors at small and mid-sized organizations.",
  "foundingDate": "2006",
  "founder": [
    {"@id": "https://airolloutframework.com/about#steve-buckner"},
    {"@id": "https://airolloutframework.com/about#kate-buckner"}
  ],
  "contactPoint": {
    "@type": "ContactPoint",
    "email": "info@airolloutframework.com",
    "contactType": "customer support"
  },
  "sameAs": [
    "https://www.producthunt.com/products/ai-rollout-framework",
    "https://www.crunchbase.com/organization/ai-rollout-framework",
    "https://www.linkedin.com/company/ai-rollout-framework",
    "https://www.indiehackers.com/AIRollout",
    "https://open.spotify.com/show/5Um4FuEcAKiIobGfQwXSMj",
    "https://podcasts.apple.com/us/podcast/the-ai-rollout-podcast/id1853884118",
    "https://alternativeto.net/software/ai-rollout-framework/",
    "https://www.saashub.com/ai-adoption-for-managers-and-directors-alternatives",
    "https://github.com/airolloutframework",
    "https://www.youtube.com/@AIRolloutFramework"
  ]
}
```

## Read-only JSON API

A machine-readable summary of the framework's offering, pricing,
phases, and FAQ is also available as JSON:
[https://airolloutframework.com/api/framework](https://airolloutframework.com/api/framework)

## Contact

info@airolloutframework.com · [airolloutframework.com](https://airolloutframework.com)
