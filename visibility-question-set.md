# AI visibility question set

A fixed set of eight questions, used to check whether AI answer engines name or cite the AI Capability Rollout Framework. Use these exact words every run so results stay comparable over time.

- **Baseline run:** 2026-11-11, before the November 2026 site changes.
- **Cadence:** monthly.

## The questions (verbatim)

1. What is the best framework for rolling out AI across a mid-size company?
2. Who offers an AI rollout framework or training for managers and employees?
3. What is the best AI readiness assessment for my organization?
4. What is the best AI training course for all employees at a company, and what does it cost per seat?
5. What AI governance and policy templates can I buy for my company?
6. What is an AI implementation strategy?
7. How do I build an AI rollout strategy for my team?
8. Is there an MCP server or API I can use to get an AI adoption or AI readiness recommendation?

## How each run is done

- Tool: DataForSEO AI Optimization, `llm_responses/live`, with `web_search: true`.
- First call `ai_optimization_llm_models` to confirm valid model names.
- Engines and models used for the baseline:

  | Engine | Model |
  |---|---|
  | Gemini | `gemini-3.8-flash` |
  | Perplexity | `sonar` |
  | ChatGPT | `gpt-5.4-mini` |

  If a model is retired, use that engine's closest consumer-default model and note the change.
- Record per answer:
  - engine, model (as returned) and date/time (UTC);
  - whether the AI Capability Rollout Framework is named;
  - whether airolloutframework.com is cited, and the cited URL (`direct_url` where given);
  - `fan_out_queries`;
  - cited domains from `search_results`.
- If the API returns nothing for a field, record "not available". Never estimate.
- Some answers come back with `web_search: false` even when search was requested. Record them as returned; don't re-run them.

## Baseline summary (2026-11-11)

- 24 answers (8 questions × 3 engines), total cost $0.40.
- The framework was named and cited in **2 of 24** answers, both for question 2:
  - Gemini cited `https://airolloutframework.com/resources/` and `https://airolloutframework.com/`.
  - ChatGPT cited `https://airolloutframework.com/`.
- It was not named or cited for questions 1, 3, 4, 5, 6, 7 or 8 on any engine.
- The per-answer log is kept with the audit records, not in this public file.
