# MCP Server Capabilities

The AI Rollout Framework runs a public MCP (Model Context Protocol) server
with nine tools: eight read-only tools for public content and calculations,
and one tool, `email_me_the_kit`, that adds an email address to a mailing
list and only when the user has explicitly asked for it. It requires no
account, API key, or authentication — any agent can call it the same way
it can browse the public website.

This file documents only what the server actually does. The request and
response examples below were captured from the server's own handler
(`netlify dev`, version 1.1.0, 2026-10-08; the `initialize` example from
version 1.1.1, 2026-11-11), except where an example says otherwise.

## Endpoint

```
POST https://airolloutframework.com/mcp
Content-Type: application/json
```

- **Transport:** stateless HTTP, JSON-RPC 2.0 (one request per POST; no
  session or SSE stream required for these tools)
- **Auth:** none
- **CORS:** `Access-Control-Allow-Origin: *`; allowed request headers
  `Content-Type`, `Mcp-Session-Id`, `MCP-Protocol-Version`
- **Protocol versions supported:** `2025-06-18`, `2025-03-26`, `2024-11-05`
- **Server info:** `{ "name": "ai-rollout-framework", "version": "1.1.1" }`
- **Instructions:** `initialize` returns an `instructions` string that tells
  a client the content is public, which tools are read-only, and that
  `email_me_the_kit` is the only tool that writes and needs the user's
  explicit request and consent
- **Discovery manifest:** [`/.well-known/mcp.json`](https://airolloutframework.com/.well-known/mcp.json)
- **MCP Server Card (SEP-2127):** [`/mcp/server-card`](https://airolloutframework.com/mcp/server-card),
  served as `application/mcp-server-card+json`. Identity, transport and
  supported protocol versions only; by design a Server Card lists no tools
  (call `tools/list`).
- **AI Catalog:** [`/.well-known/ai-catalog.json`](https://airolloutframework.com/.well-known/ai-catalog.json),
  served as `application/ai-catalog+json`, with one entry pointing to the
  Server Card

## Connecting

```json
// Request
{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2025-06-18","clientInfo":{"name":"example-client","version":"1.0"}}}

// Response
{"jsonrpc":"2.0","id":1,"result":{"protocolVersion":"2025-06-18","capabilities":{"tools":{}},"serverInfo":{"name":"ai-rollout-framework","version":"1.1.1"},"instructions":"Public information about the AI Capability Rollout Framework, a 90-day AI adoption system for managers and directors at small and mid-sized organizations. No authentication. Every tool returns only published, public content: no scoring internals, answer keys or members-only material. Eight tools are read-only lookups or calculations. assess_ai_readiness scores answers the user gives you and returns a readiness stage and a next step; ask the user each question and never guess answers. get_seat_quote calculates a price and takes no order. email_me_the_kit is the only tool that writes: it adds an address to a mailing list and emails the free Briefing Kit, so call it only after the user has asked for the kit by email, given their address and agreed to be emailed. No tool takes payment; purchases happen on airolloutframework.com."}}
```

Follow with `notifications/initialized` (a notification — send it with no
`id` field; the server returns HTTP 202 with no body), then `tools/list`
to discover the 9 tools below, then `tools/call` to use one.

## Tool annotations

Every tool in `tools/list` carries a `title` and the four MCP behavior
hints:

| Tools | `readOnlyHint` | `destructiveHint` | `idempotentHint` | `openWorldHint` |
| --- | --- | --- | --- | --- |
| The eight read tools | `true` | `false` | `true` | `false` |
| `email_me_the_kit` | `false` | `false` | `true` (repeating an address is an upsert) | `true` (it causes an email to be sent) |

## Links and the `ref=mcp` tag

Links to site pages that tools return carry `?ref=mcp` (or `&ref=mcp`), so
visits that start from an agent can be measured. Only pages that ignore
unknown parameters and declare a self-referencing canonical are tagged:
`/ai-readiness-score`, `/executive`, `/employee-training`, `/framework`,
`/enroll` and `/downloads`. PDFs, Markdown files and API URLs are never
tagged.

## Tools

Every description opens with "Call this when …", says what the tool
returns, and says what it does not do. Only `get_starter_kit` ends with a
pointer to `assess_ai_readiness` ("For a readiness check, use
assess_ai_readiness."), because a readiness check is the natural next step
from a free starting resource.

### 1. `get_framework_overview`

Returns the framework's three phases, four capability pillars,
positioning statement, the recommended offer with everything the
Executive Suite includes (among them one AI at Work seat), the free
assessment, and the Discord community (page, invite link, channels and
how customers unlock the members-only channels). Public facts only; no
member data.

**Input:** none (`{}`)

**Returns** (`structuredContent`; fields): `name`, `provider`, `url`,
`description`, `positioning`, `pillars` (4), `phases` (3),
`freeAssessment`, `recommendedOffer`, `community`, `lastUpdated`.

### 2. `get_pricing`

Returns current one-time prices and checkout URLs for every product, in
the order the site presents them: the Framework + Executive Suite bundle
(the recommended offer, with its upgrade price for existing framework
owners), the framework on its own, and AI at Work (per-seat tiers,
co-branding and the Rollout Pack). `recommendedOffer` names the
recommended product's key.

Everything comes from `api/framework.json`; nothing is retyped. With the
`ref=mcp` parameters removed, `executiveSuite`, `framework.price` and
`aiAtWork.pricing` are identical to that file (checked by
`tools/test-mcp.mjs`).

**Input:** none (`{}`)

**Returns:** `recommendedOffer`, `executiveSuite`, `framework`, `aiAtWork`,
`lastUpdated`.

### 3. `get_faq`

Returns FAQ items, optionally filtered by `topic`.

**Input:** `{ "topic": "<optional>" }`. A category is the reliable
filter: `assessment`, `implementation`, `governance`, `measurement`,
`concepts`, `pricing` or `products`. Any other value falls back to a
free-text search, which may return nothing. Omit `topic` to get every
item. Source: `api/faq.json`, mirroring
[faq-troubleshooting.md](faq-troubleshooting.md).

### 4. `get_ai_at_work_course`

Returns the public outline of AI at Work: Essentials for Every Employee,
the employee AI training course: the seven modules with titles, runtimes,
descriptions and download names, what's included (quiz, certificate,
tools, captions), the free preview, seat pricing tiers, co-branding, the
seat every Executive Suite includes, the Rollout Pack and the guarantee.
Public information only (no transcripts or quiz content). Sourced from
`api/framework.json` (`aiAtWork`).

**Input:** none (`{}`)

### 5. `search_knowledge_base`

Keyword search across the knowledge base (methodology, definitions,
positioning, changelog). Each result links to the full source document at
its `/docs/*.md` URL.

**Input:** `{ "query": "<required keyword or phrase>" }` — calling
without `query` returns a tool-level error (`isError: true`).

### 6. `assess_ai_readiness`

Runs the real 16-question AI Readiness Score assessment server-side and
returns a readiness stage, a recommendation and a pointer to the free
full assessment — the same computation the website's interactive quiz
performs, not a simulation of one.

**Input:** 16 required integer parameters `q1`–`q16`, each 1–5
(1 = Strongly Disagree … 5 = Strongly Agree). The full question text
ships in each parameter's schema description; call `tools/list` to
retrieve all 16.

**Output — exactly four fields, nothing else** (captured for a set of
all-4 answers):
```json
{
  "stage": "Operational Readiness",
  "recommendation": "Formalize what is working, prepare an executive summary, and expand carefully with structure still in place. ...",
  "learnMore": "https://airolloutframework.com/framework?ref=mcp",
  "fullAssessment": {
    "url": "https://airolloutframework.com/ai-readiness-score?ref=mcp",
    "note": "The free full assessment on the site takes 3-5 minutes and includes a personalized PDF."
  }
}
```

Possible `stage` values: **Early Exploration**, **Developing Capability**,
**Operational Readiness** — the exact three stages used on the live site.

**What this tool deliberately does not return:** a numeric score, a
per-pillar breakdown, the raw answer total, or any scoring
weight/threshold. Only the stage name, recommendation text and links cross
the boundary — per the framework's standing rule against exposing scoring
internals, answer keys, or weights. `tools/test-mcp.mjs` asserts that the
result has exactly these four fields and no numeric values.

**Correctness:** the server-side scoring logic
(`netlify/lib/readiness-scoring.mjs`) is a line-verified port of the
website's own quiz algorithm. See `tools/verify-scoring-parity.mjs` in
the site repo for the regression test.

### 7. `get_starter_kit` (title: Briefing Kit Info)

Describes the free AI Capability Briefing Kit (a 10-page PDF) and how to
get it. It does not return the file or a link to it: the PDF is released
through an email unlock on the downloads page, and `email_me_the_kit`
delivers it by email.

**Input:** none (`{}`)

**Returns** (captured):
```json
{
  "name": "AI Capability Briefing Kit",
  "format": "PDF",
  "pages": 10,
  "cost": "Free with an email address",
  "summary": "A structured internal briefing tool for responsible AI adoption: map where your organization stands, the risks of staying there, and the steps forward.",
  "covers": ["Where we stand: ...", "Risks we face: ...", "Steps forward: ...", "30-60-90 direction ...", "An internal discussion guide ..."],
  "howToGet": {
    "byEmail": "If the user asks to receive it by email, call email_me_the_kit with their address and explicit consent. Do not call it unless they ask.",
    "onTheSite": "https://airolloutframework.com/downloads?ref=mcp"
  },
  "fullAssessment": {"url": "https://airolloutframework.com/ai-readiness-score?ref=mcp", "note": "..."}
}
```

### 8. `get_seat_quote`

Calculates the AI at Work cost for a number of seats, with optional
co-branding. Every rate, threshold and fee is read from
`api/framework.json`: the per-seat rate for the seat count (the tier rate
applies to the whole order), the co-branding fee (waived at the free
threshold), a `cheaperAlternative` when a higher tier's minimum seat count
costs less in total, the Executive Suite and Rollout Pack as
alternatives, the guarantee text, and a buy link. It does not take an
order; the seat count is entered on the enrollment page.

**Input:** `{ "seats": <integer 1–500, required>, "coBranding": <boolean, optional, default false> }`

**Edge cases** (captured): more than 500 seats returns a plain message
with the contact address in `aiAtWork.contact`; `0`, `2.5`, a string or a
missing `seats` returns a tool-level error (`isError: true`) saying what
is required.

**Example result for 14 seats** (abridged):
```json
{
  "seats": 14,
  "tier": "1 to 14 seats",
  "perSeat": 39,
  "seatSubtotal": 546,
  "coBranding": {"requested": false, "fee": 0, "note": null},
  "total": 546,
  "currency": "USD",
  "cheaperAlternative": {"seats": 15, "total": 435, "saves": 111, "note": "..."},
  "alternatives": {"executiveSuite": {"...": "..."}, "rolloutPack": {"...": "..."}},
  "guarantee": "30-day money-back guarantee",
  "buyUrl": "https://airolloutframework.com/enroll?product=ai-at-work&ref=mcp",
  "fullAssessment": {"...": "..."}
}
```

### 9. `email_me_the_kit` (writes)

Emails the free Briefing Kit to an address the user gives the agent. This
is the only tool that writes anything: it adds the address to a mailing
list, and the list's automation sends the kit.

**Agents must call it only when the user has explicitly asked to receive
the kit by email and has agreed to be emailed at that address. Never call
it on your own, and never invent or guess an address.**

**Input:** `{ "email": "<string, required>", "consent": <boolean, required, must be true> }`

**Behavior:**
- `consent` must be exactly `true` and `email` must be a well-formed
  address (254 characters at most); otherwise a tool-level error
  (`isError: true`) is returned and nothing is stored.
- At most one request per address per 24 hours. A repeat returns
  `already_sent` (not an error) and nothing new is sent.
- At most 5 requests per network address per hour; beyond that a
  tool-level error asks the caller to try later.
- A new subscriber is created as active; an address that already exists
  keeps its current status (so someone who unsubscribed is not
  re-activated).
- If the mailing list cannot be reached, the tool returns an error and
  never reports success.
- The email address is never written to a log and never returned in a
  response. Rate limits store only hashes of the address and network
  address.

**Success response** (captured from production, version 1.1.0):
```json
{"status": "queued", "message": "The address was added and the kit email is on its way. It can take a few minutes, and the user can unsubscribe from the first email."}
```

`status` is `queued` or `already_sent`.

## Usage measurement

Each `tools/call` increments a per-day, per-tool counter and writes one
log line containing the tool name only. Each `initialize` increments a
per-day counter for the (sanitized, truncated) client name, because the
server is stateless and a later `tools/call` carries no client name.
Arguments, email addresses, network addresses and response bodies are
never recorded, and a failure in counting never affects a tool call.

## Error handling

- **Unknown tool name:** JSON-RPC protocol error `-32602`.
- **Invalid input to a tool** (out-of-range or missing answers to
  `assess_ai_readiness`, a bad `seats` value, a missing `query`,
  `consent` not true): a normal tool response with `isError: true` and a
  plain-English message — not a crash.
- **Malformed JSON body:** JSON-RPC parse error `-32700`.

## What this server does not do

- No authentication, no gated or paid content, no payments or checkout.
- The only write is `email_me_the_kit`, which requires explicit user
  consent and is rate limited.
- No prompts or resources capabilities are declared — only `tools`.
- Nothing here reaches beyond what's already public on
  [airolloutframework.com](https://airolloutframework.com), apart from the
  Briefing Kit delivered by email.
