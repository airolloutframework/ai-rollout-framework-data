# MCP Server Capabilities

The AI Rollout Framework runs a public MCP (Model Context Protocol) server
exposing read-only content and one computation tool. It requires no
account, API key, or authentication — any agent can call it the same way
it can browse the public website.

This file documents only what is actually live and tested. Every example
below is a real request/response pair captured from the live server on
2026-08-20, not a hypothetical.

## Endpoint

```
POST https://airolloutframework.com/mcp
Content-Type: application/json
```

- **Transport:** stateless HTTP, JSON-RPC 2.0 (one request per POST; no
  session or SSE stream required for these tools)
- **Auth:** none
- **CORS:** `Access-Control-Allow-Origin: *`
- **Protocol versions supported:** `2025-06-18`, `2025-03-26`, `2024-11-05`
- **Server info:** `{ "name": "ai-rollout-framework", "version": "1.0.0" }`

## Connecting

```json
// Request
{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2025-06-18","clientInfo":{"name":"example-client","version":"1.0"}}}

// Response (captured live, 2026-08-20)
{"jsonrpc":"2.0","id":1,"result":{"protocolVersion":"2025-06-18","capabilities":{"tools":{}},"serverInfo":{"name":"ai-rollout-framework","version":"1.0.0"}}}
```

Follow with `notifications/initialized` (a notification — send it with no
`id` field; the server returns HTTP 202 with no body), then `tools/list`
to discover the 5 tools below, then `tools/call` to use one.

## Tools

### 1. `get_framework_overview`

Returns the AI Capability Rollout Framework's three implementation
phases, four capability pillars, and core positioning statement.

**Input:** none (`{}`)

**Example call:**
```json
{"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"get_framework_overview","arguments":{}}}
```

**Returns** (`structuredContent`, live-verified fields):
```json
{
  "name": "AI Capability Rollout Framework",
  "description": "...",
  "positioning": "Responsible AI adoption starts with capability, not technology.",
  "pillars": [
    {"name": "Strategy & Leadership Clarity", "description": "..."},
    {"name": "Governance & Risk Awareness", "description": "..."},
    {"name": "Workflow Integration", "description": "..."},
    {"name": "Capability & Skill Development", "description": "..."}
  ],
  "phases": [
    {"name": "Establish Clarity & Guardrails", "days": "1-30", "description": "..."},
    {"name": "Controlled Pilot", "days": "31-60", "description": "..."},
    {"name": "Measure, Formalize & Scale", "days": "61-90", "description": "..."}
  ],
  "freeAssessment": {"name": "AI Readiness Score", "url": "https://airolloutframework.com/ai-readiness-score", "duration": "3-5 minutes"}
}
```

Source: `api/framework.json` (the same file backing the existing
[`/api/framework`](https://airolloutframework.com/api/framework) endpoint) — read directly, not duplicated.

### 2. `get_pricing`

Returns current pricing and checkout URLs for both products.
**Highest drift-risk tool** — sourced live from `api/framework.json`, the
same file flagged for inclusion in any future pricing-consistency audit.

**Input:** none (`{}`)

**Example call and real response** (captured live, 2026-08-20):
```json
// Request
{"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"get_pricing","arguments":{}}}

// structuredContent
{
  "framework": {
    "name": "AI Capability Rollout Framework",
    "price": {"amount": 99, "currency": "USD", "type": "one-time"},
    "checkoutUrl": "https://airolloutframework.com/enroll",
    "url": "https://airolloutframework.com/framework"
  },
  "teamTraining": {
    "name": "The Complete AI Learning Path (4-Course Master Bundle)",
    "price": {"amount": 24.99, "currency": "USD", "type": "one-time", "perSeat": true},
    "checkoutUrl": "https://airolloutframework.com/enroll?product=team-training",
    "url": "https://airolloutframework.com/employee-training"
  },
  "lastUpdated": "2026-08-20"
}
```

### 3. `get_faq`

Returns FAQ items (14 total), optionally filtered by keyword.

**Input:** `{ "topic": "<optional keyword>" }`

**Example:** `{"name":"get_faq","arguments":{"topic":"shadow"}}` returns 1
matching item (the shadow-AI governance question). Omitting `topic`
returns all 14 items. Source: `api/faq.json`, mirroring
[faq-troubleshooting.md](faq-troubleshooting.md).

### 4. `search_knowledge_base`

Keyword search across the AI Rollout Framework knowledge base
(methodology, definitions, positioning, changelog). Each result links to
the full source document at its `/docs/*.md` URL.

**Input:** `{ "query": "<required keyword or phrase>" }` — calling
without `query` returns a tool-level error (`isError: true`), verified.

**Example:** `{"name":"search_knowledge_base","arguments":{"query":"capability-first"}}`
returns matching sections from `entity-definitions.md` and
`positioning-comparison.md`, each with a `url` back to the full file.

### 5. `assess_ai_readiness`

Runs the real 16-question AI Readiness Score assessment server-side and
returns a readiness stage and recommendation — the same computation the
website's interactive quiz performs, not a simulation of one.

**Input:** 16 required integer parameters `q1`–`q16`, each 1–5
(1 = Strongly Disagree … 5 = Strongly Agree). The full, real question
text ships in each parameter's schema description — call `tools/list` to
retrieve all 16 verbatim questions grouped by pillar (Strategy &
Leadership Clarity, Governance & Risk Awareness, Workflow Integration,
Capability & Skill Development).

**Output — exactly 3 fields, nothing else:**
```json
{
  "stage": "Operational Readiness",
  "recommendation": "Formalize what is working, prepare an executive summary, and expand carefully with structure still in place. The AI Capability Rollout Framework — including the AI Capability Pilot Builder — turns readiness into a repeatable operating approach rather than one successful pilot.",
  "learnMore": "https://airolloutframework.com/framework"
}
```
(Real response, captured live 2026-08-20, for a test set of all-4 answers.)

Possible `stage` values: **Early Exploration**, **Developing Capability**,
**Operational Readiness** — the exact three stages used on the live site.

**What this tool deliberately does not return:** a numeric score, a
per-pillar breakdown, the raw answer total, or any scoring
weight/threshold. Only the stage name and recommendation text cross the
boundary — per the framework's standing rule against exposing scoring
internals, answer keys, or weights. This was verified with an automated
scan of every tool response and the `tools/list` schema text itself for
any of those terms; none were found.

**Correctness:** the server-side scoring logic
(`netlify/lib/readiness-scoring.mjs`) is a line-verified port of the
website's own quiz algorithm — not a re-guess at it. Two independent
answer sets were run through both the live quiz page and this tool; both
returned identical stage results (a "Developing Capability"-adjacent
mixed pattern → **Operational Readiness**; an all-"Strongly Disagree" set
→ **Early Exploration**). See `tools/verify-scoring-parity.mjs` in the
site repo for the regression test.

## Error handling

- **Unknown tool name:** JSON-RPC protocol error `-32602`.
- **Invalid/out-of-range/missing answers to `assess_ai_readiness`:** a
  normal tool response with `isError: true` and a plain-English message
  naming which answers were missing or invalid — not a crash.
- **Malformed JSON body:** JSON-RPC parse error `-32700`.

## What this server does not do

- No authentication, no rate limiting beyond what Netlify applies
  platform-wide, no write access, no gated or paid content.
- No prompts or resources capabilities are declared — only `tools`.
- Nothing here reaches beyond what's already public on
  [airolloutframework.com](https://airolloutframework.com).
