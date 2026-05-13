# Migration Readiness Pilot — Architecture & Design

> A pre-cutover healthcheck for cloud migrations. Single HTML file. BYOK. Built on the same skeleton as EM Cockpit, with four upgrades that matter.

**Prepared:** May 2026
**Project repo:** `migration-readiness-pilot/`
**Sibling tool:** EM Cockpit (same skeleton, different vertical)

---

## 1. One-paragraph summary

Migration Readiness Pilot is a single-page web tool that converts a free-form migration state (source environment, target environment, scope, SLOs, known risks) into a structured pre-cutover briefing in roughly two seconds. The output is a verdict (GO / CONDITIONAL GO / NO-GO) with a confidence percentage, a list of P0/P1/P2 blockers with remediations, an 8-dimension scorecard, and a pre-cutover checklist ordered by T-minus days. There is no backend, no build step, no database, and no telemetry. The entire tool is one HTML file (~700 lines, including CSS and JavaScript).

---

## 2. The five layers

The architecture is a strict five-layer pipeline that runs entirely in the user's browser. Each layer has one job and one output contract, which is what keeps the code under 250 lines of script.

### Layer 1 — Input

Two active panes and one disabled-on-purpose pane. The Form pane has seven structured fields (source, target, scope, SLOs, team, known risks, free-form notes). The Paste pane is a single textarea for unstructured material — a runbook, an ADR, a Jira export. The Connectors pane is visible but disabled to signal roadmap without committing to four OAuth integrations.

A click on a tab swaps `pane.active` and updates `state.tab`. That's the entire input layer's logic.

### Layer 2 — Orchestration

Three pure-ish functions in sequence: `collectInput()` reads the active pane and returns one string; `buildPrompt(input)` wraps it in a persona, the strict JSON schema, and the verdict rules; the `dispatcher` map selects which provider adapter receives the prompt. The dispatcher is one line:

```js
const dispatcher = { groq: callGroq, openai: callOpenAI, anthropic: callAnthropic };
const raw = await dispatcher[state.provider](key, buildPrompt(input));
```

This is the only place provider selection matters. Adding Gemini, DeepSeek, or a local Ollama endpoint is one new adapter function and one new key in the map.

### Layer 3 — Provider adapters (BYOK)

Three async functions — `callGroq`, `callOpenAI`, `callAnthropic` — each with the same input contract (`key, prompt`) and the same output contract (a JSON string). Each adapter is ~15 lines: build the fetch payload in that provider's request shape, await the response, throw on non-200, return the message content.

The API key is read from a password-masked form field, passed into the adapter as a function argument, and used in a single `fetch()` call to the provider. It is never stored, never echoed to any server, and never written to `localStorage` or `sessionStorage`. Closing the tab destroys it.

### Layer 4 — Response

`JSON.parse(raw)` plus a defensive read of the expected shape. The parsed object becomes `state.lastReport` — held in memory for the rest of the session, used by the renderer and by the "Copy as Markdown" export.

### Layer 5 — Render

Four `innerHTML` writes into four DOM regions: a verdict banner that re-themes itself based on the GO/CONDITIONAL/NO-GO classification, a list of blocker cards (color-coded by severity), an 8-row scorecard with animated horizontal bars, and a clickable checklist where each item can be ticked off (in-memory only, no persistence). One `esc()` helper handles HTML escaping; that's the entire XSS surface.

---

## 3. Why each design choice won

Every architectural decision was made against one of three criteria: zero maintenance, zero deploy friction, or zero output drift. The trade-offs below explain the path not taken.

| Decision | Alternative | Why this won |
|---|---|---|
| Single HTML file | React + Vite, Vercel | No toolchain rot. Forkable in 30 seconds. Source is the artifact. |
| BYOK | Proxy through Cloudflare Worker | No billing system, no rate-limiter, no abandoned-project decay. |
| JSON-mode output | Free-form prose + post-hoc parsing | Render code is ~70 lines. Output shape is identical across providers. |
| Three-provider dispatcher | Pick one provider | Reader ships on the model they already pay for. Trivial fourth. |
| Form + Paste, no live connectors | OAuth for GitHub/Linear/Jira | Connectors are 80% of maintenance for 20% of unique value. |
| In-memory state only | localStorage with "clear" button | Removes the entire privacy surface. Close the tab; nothing leaks. |

---

## 4. The four upgrades over EM Cockpit

Same skeleton, four meaningful differences. Each one is a paragraph because each one carries its own lesson.

### 4.1 Verdict logic encoded in the prompt, not the code

The most important design decision in the tool. The prompt explicitly tells the model: *"Verdict logic: GO only if zero P0 blockers AND no scorecard dimension <60. CONDITIONAL GO if 1–2 P0 with named remediation. NO-GO if 3+ P0 or any dimension <40."* This is a load-bearing constraint. Without it, models default to optimism — they want to please the user and tend to call things "ready" when they aren't. By encoding the math in natural language inside the prompt, the verdict becomes mechanically honest, and the model has to surface the P0s that force a CONDITIONAL or NO-GO call.

### 4.2 Fixed 8-dimension scorecard

The scorecard has the same eight dimensions in every report, in the same order — Network, IAM, Database, Compute, Security, Observability, DR/Backup, Operations. This single decision is what turns a one-off tool into an organizational asset. Two migrations scored against the same eight dimensions are *comparable*, which means you can finally answer the question "is this migration in worse shape than the last one was at T-14?" The model can be wrong about any individual score; it can't be wrong about the shape of the answer.

### 4.3 Verdict banner re-themes by severity

Three CSS classes — `.go`, `.conditional`, `.nogo` — change the verdict banner's accent strip and text color. This is a 12-line visual treatment that does more for credibility than any other piece of UI. A red banner cannot be misread; a green one earns the audience's trust because the model has to defend a green call against the verdict rules in the prompt.

### 4.4 Copy as Markdown export

The lone "viral loop" feature. After a report renders, an `Export` button generates a clean Markdown version (headings, lists, blockers with remediations, the full checklist with T-minus dates) and writes it to the clipboard. This is what makes the tool spread — the user pastes the report into Confluence, Slack, or a Jira ticket, and the formatted version arrives with credit baked in.

---

## 5. The prompt is the product

This is worth re-stating because it's the single most copyable lesson from the project. The interesting block of code is not the dispatcher, not the adapters, not the renderer. It is `buildPrompt()`. The prompt does five things that the rest of the code can't:

It pins a persona in the first sentence (*"You are a senior cloud-migration architect and the user's chief-of-staff"*). It shows the model the exact JSON shape with placeholder values, not just a description — models follow examples better than instructions. It enforces the verdict math (zero P0 + no dimension <60 = GO) so the model can't quietly hand-wave a green light. It gives negative rules at the end (*"Be specific. Use the input verbatim where useful."*) — negative rules stop the most common failure modes. And it locks the scorecard to all eight dimensions, in order, so the report is structurally comparable across runs.

If you fork this skeleton into a different tool, this is the file you actually rewrite. Everything else is reused as-is.

---

## 6. Design system (in one screen)

The visual system is small and opinionated, which is what makes any sibling tool in the portfolio still look like the same family.

**Three rules.** Mono for labels, sans for body, never the other way around. Letter-spacing on every uppercase label (0.14em–0.22em) — without it, all-caps reads as shouty. Accent gradient appears in exactly one place: the brand mark. Everywhere else, accent is a flat color.

**Nine tokens.** Background (`#06080d`), card surface (`#10151f`), two ink levels (`#e9eef7` / `#8a95aa`), accent mint (`#7cf7d2`), accent violet (`#9d8cff`), warn amber (`#ffb86b`), bad rose (`#ff7a8a`), good lime (`#8af0a0`). That's the whole palette.

**One container.** The card pattern — 22px padding, 14px radius, 1px line border, soft outer shadow — is used for both the input panel and the output panel. That's what visually pairs them and removes the need for any other layout decision.

---

## 7. Forking the skeleton

To turn this tool into another in the series, three things change. Everything else is reused.

**Change the prompt persona and JSON shape.** Edit `buildPrompt()`. Replace the role line, the strict-JSON schema, and the rules. For an SOC2 Audit Pre-Check, for example, the schema becomes `controls[]`, `evidence_gaps[]`, `auditor_questions[]`, `verdict`.

**Rename the form fields.** Seven fields and one notes textarea. Rename their `id` attributes and labels. `collectInput()` reads whatever IDs exist, so no JS changes are needed.

**Update the four output regions.** Inside the result div, change the four section headers and the four `innerHTML` blocks in `render()` to match the new JSON keys. Roughly 25 lines change.

Everything else — provider adapters, key field, demo fallback, design tokens, deploy story, Markdown export — is reused as-is. Average fork time is 30 minutes once the first tool ships.

---

## 8. What's intentionally missing

Three things readers will notice are absent, and the reasoning matters.

There is no authentication. Adding auth would require a backend, which would require deployment, which would require monitoring, which would require billing. Skipping auth is what makes the tool maintainable forever.

There is no persistence. Refreshing the page wipes the report. This is by design — persistence implies a place where reports live, which implies access control, which implies the whole auth chain above. The Markdown export is the persistence layer; the user owns it.

There are no real connectors. The Connectors tab is visible and disabled because (a) live OAuth integrations are 80% of the maintenance cost for 20% of the differentiated value, and (b) signaling roadmap is cheaper than delivering it. If a v2 connector ships, it will be one Cloudflare Worker that reads a single resource (e.g., recent Jira tickets in a label) and pastes them into the Form pane — not a full sync.

---

## 9. Roadmap

The smallest set of additions that would genuinely move the tool forward, in order of payoff:

**v1.1** — Save report to clipboard as `.md` *and* as a downloadable file. Same export logic, second target.

**v1.2** — Diff mode. Two reports side-by-side, each dimension highlighted if the score moved more than ±10. This is what unlocks the "are we trending up or down" question.

**v2.0** — One Cloudflare Worker, one connector. The cheapest possible integration: pull a label-filtered Jira query and prepend the titles to the input string. No two-way sync.

**v2.1** — Custom 8-dimension definitions per org, read from a YAML config in the repo. Lets a team tune the scorecard without forking.

**v3.0** — Multi-target healthcheck. Score the same workload against three candidate target platforms in one run, return a comparison matrix. This is the version that gets the second LinkedIn post worth writing.

---

*End of document — Migration Readiness Pilot v1.0, architecture & design brief.*
