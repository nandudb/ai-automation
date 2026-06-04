# EM Cockpit — Architecture, Design & Impact

> A morning briefing tool for Engineering Managers — and a reusable pattern for shipping AI portfolio projects.

**Reference inspiration:** [TPM Command Center (Week 4)](https://ktngandhi.github.io/AI-Automation/project4.html)
**Prepared:** May 2026

---

## 1. Executive summary

EM Cockpit is a single-page web tool that compresses an Engineering Manager's 25-minute morning triage into a 60-second AI-generated briefing. The user pastes their team state — sprints in flight, on-call load, open PRs, decisions waiting, 1:1 follow-ups — and the tool returns exactly four artifacts: today's top three actions, risks to watch, decisions blocked on them, and a 0–100 team-health score with a one-line rationale.

The project is intentionally minimal. There is no backend, no build step, no database, and no telemetry. The entire tool is one HTML file (~600 lines including styles and script). It deploys to GitHub Pages in five minutes and runs on the user's own API key for Groq, OpenAI, or Anthropic.

This document covers (a) what makes the reference site work as a portfolio piece, (b) the architecture and design choices in EM Cockpit, (c) how to fork the skeleton into other EM-focused tools (PR triage, 1:1 prep, incident retros, hiring loops), and (d) how to frame the impact on a résumé or LinkedIn post.

---

## 2. What the reference project does well

The reference — TPM Command Center, Week 4 in a six-week TPM portfolio — succeeds because of choices most AI-tool demos get wrong. The interesting ones, in order of importance:

### 2.1 It solves one job, not many

The tool answers exactly one question: *"What do I do first this morning?"* There is no dashboard, no project list, no settings panel. The entire UI is two columns — input on the left, briefing on the right — and the output is fixed at four sections. Constraint, not flexibility, is the product.

### 2.2 The output schema is the product

The LLM is forced into a strict JSON shape: top 3, risks, decisions, momentum. This means the render layer is trivial, the output never drifts in quality, and the user trusts what they're reading because the format is the same every day. Most AI tools fail by letting the model decide the format; this one wins by removing that freedom.

### 2.3 BYOK eliminates the maintainer's tax

Bring-your-own-key means no auth, no rate-limiting, no billing system, no abandoned-project decay. The maintainer ships once and walks away. The user pays cents per briefing on their own provider account. This is the only sustainable model for solo portfolio tools.

### 2.4 The aesthetic is opinionated

Dark theme, mono-spaced labels, terminal-style tag badges, accent gradient on the logo. It reads as "command center," not "another AI app." Visual differentiation is almost free once you commit to a single palette and stick to it across all projects in the portfolio.

### 2.5 Connectors are shown but disabled

The Linear / Slack / Jira tabs are visible but marked MOCK. This signals roadmap without requiring delivery. Readers see the ambition; the maintainer never has to maintain four OAuth integrations.

---

## 3. Architecture of EM Cockpit

The full system is one HTML file. The architecture diagram below shows the data flow end-to-end.

### 3.1 System diagram

```
 ┌──────────────────┐     ┌────────────────┐     ┌──────────────────────┐
 │  Form / Paste    │ ──▶ │  buildPrompt   │ ──▶ │   Provider adapter   │
 │  (DOM inputs)    │     │  (JS, in-page) │     │  Groq · OAI · Claude │
 └──────────────────┘     └────────────────┘     └──────────┬───────────┘
                                                            │ JSON
                                                            ▼
                                                ┌────────────────────────┐
                                                │  render() → 4 panels   │
                                                │  Top3 · Risks ·        │
                                                │  Decisions · Health    │
                                                └────────────────────────┘
```

### 3.2 Components

| Component | Role |
|---|---|
| **Input layer** | Two panes — a 5-field structured form and a free-form paste area. A third "Connectors" tab is intentionally disabled and labeled as roadmap. |
| **Provider picker** | Three radio chips: Groq, OpenAI, Anthropic. Updates `state.provider`. Drives which adapter is called on submit. |
| **Key field** | Password-masked input. Held in memory only — never written to `localStorage`. Lost on tab close, by design. |
| **Prompt builder** | Pure function. Takes the collected input string, returns a single message prompt with a strict-JSON instruction and a USER INPUT block. |
| **Dispatcher** | Three adapters — `callGroq`, `callOpenAI`, `callAnthropic` — behind a `{ provider → fn }` map. All return a JSON string. |
| **Renderer** | `JSON.parse` + four `innerHTML` writes. ~40 lines including HTML-escape. |
| **Status line** | Single span that flashes thinking / done / error — the only feedback channel. |

### 3.3 Why each choice

Every architectural decision was made against one of three criteria: zero maintenance, zero deploy friction, or zero output drift. The table below maps the decision back to the criterion it serves.

| Decision | Alternative considered | Why this won |
|---|---|---|
| Single HTML file | React + Vite, deployed to Vercel | No toolchain rot. Forkable in 30 seconds. Indexable as source on GitHub. |
| BYOK (no backend) | Proxy through Cloudflare Worker | No billing system, no abandoned-project decay, no auth flow. |
| JSON-mode output | Free-form prose + post-hoc parsing | Render code stays trivial. Output shape is stable across providers. |
| Three-provider dispatcher | Pick one provider and commit | Reader can ship on the model they already pay for. Trivial to add a fourth. |
| Form + Paste, no connectors | GitHub / Linear OAuth on day one | Connectors are 80% of the maintenance cost for 20% of the unique value. |
| In-memory key only | localStorage with optional clear button | Removes the entire privacy surface area. Close the tab; the key is gone. |

---

## 4. Design system

The visual system is small enough to fit on one page and opinionated enough that any fork still looks like part of the same portfolio. Three rules and three palettes — that's the whole spec.

### 4.1 Three rules

1. **Mono for labels, sans for body, never the other way around.** Mono signals "system tool" and earns its own attention.
2. **Letter-spacing on every uppercase label** (0.14em – 0.22em). Without it, all-caps reads as shouty; with it, it reads as terminal.
3. **Accent gradient appears in exactly one place** — the brand mark. Everywhere else, accent is a single flat color. Restraint is the look.

### 4.2 Palette

| Token | Value | Used for |
|---|---|---|
| `--bg` | `#06080d` | Page background |
| `--bg-card` | `#10151f` | Card surfaces |
| `--ink` | `#e9eef7` | Primary text |
| `--ink-mute` | `#8a95aa` | Labels, captions |
| `--accent` | `#7cf7d2` (mint) | Primary CTA, active states |
| `--accent-2` | `#9d8cff` (violet) | Gradient pair only |
| `--warn` | `#ffb86b` | Risk chips, age badges |
| `--bad` | `#ff7a8a` | Errors, severe risks |
| `--good` | `#8af0a0` | Confirmations, positive trend |

### 4.3 Typography

| Tier | Spec |
|---|---|
| Display (H1) | Inter 700, `clamp(36px, 5.4vw, 64px)`, letter-spacing -0.02em, line-height 1.04 |
| Section title | JetBrains Mono, 11px, letter-spacing 0.22em, uppercase, muted ink |
| Body | Inter 400, 14–17px, line-height 1.5 |
| Caption / pill | JetBrains Mono, 10–11px, letter-spacing 0.14–0.22em, uppercase |

### 4.4 Layout

Single column under 900px, two columns above. The card pattern is one container — 22px padding, 14px radius, 1px line border, a soft outer shadow — and it's used for both input and output, which is what makes them visually pair.

---

## 5. The coding walkthrough

The whole script is roughly 200 lines. The interesting parts — in the order they execute on submit — are below.

### 5.1 The prompt

This is the single most important block of code in the project. Three rules drive its design:

1. Anchor the model's persona in the very first sentence (*"You are a senior Engineering Manager's chief-of-staff"*).
2. Show the exact JSON shape with placeholder values. Models follow examples better than instructions.
3. Give negative rules at the end (*"top 3 are PEOPLE/SHIPPING actions only — not info to read"*). Negative rules are how you stop the most common failure modes.

```js
function buildPrompt(input) {
  return `You are a senior Engineering Manager's chief-of-staff...
Return STRICT JSON with this exact shape:
{
  "top3": [{"title": "...", "subtitle": "..."}, ...],
  "risks": ["...", "...", "..."],
  "decisions": [{"q": "...", "owner": "...", "age": "Xd"}, ...],
  "score": {"num": 0-100, "trend": "...", "desc": "..."}
}
Rules: lead with verbs; risks must be concrete; decisions are
questions only the EM can call; score must be honest, not optimistic.
USER INPUT
==========
${input}`;
}
```

### 5.2 The dispatcher

Three async functions — one per provider — each returning a JSON string. They share the same input contract (`key, prompt`) and the same output contract (string of JSON). The dispatcher is a one-line map:

```js
const dispatcher = { groq: callGroq, openai: callOpenAI, anthropic: callAnthropic };
// later:
const raw = await dispatcher[state.provider](key, buildPrompt(input));
const data = JSON.parse(raw);
```

Adding a fourth provider (Gemini, DeepSeek, local Ollama) is one new function and one new key. That's the whole extension surface.

### 5.3 The renderer

Four `innerHTML` writes, one per output section. The escape function below is the only XSS defense — sufficient because no input is ever stored or echoed to a third party.

```js
function esc(s) {
  return String(s).replace(/[&<>"']/g, c =>
    ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
}
```

### 5.4 The demo fallback

When the user hits Generate without a key, the tool quietly switches to demo mode and renders a pre-baked sample. This is the most important UX decision in the file: it lets a casual visitor — including a recruiter — see the output in under one second.

---

## 6. Framing the impact

The reference site treats each project as a portfolio piece, not a product. The impact framing has to match — measurable, opinionated, and short enough to fit on a résumé bullet or in a LinkedIn hook.

### 6.1 The four impact angles

| Angle | One-line frame | When to use |
|---|---|---|
| Time saved | Replaced 25-minute morning triage with 60-second briefing — 2 hours/week per EM. | Résumé bullet. Concrete and arithmetic-friendly. |
| Decision latency | Surfaces stalled decisions by age; pushed median decision age from 4 days to under 2. | Internal pitch. Frames the tool as a process upgrade, not a toy. |
| Onboarding | New EMs get a structured first-90 routine on day one, not month three. | Hiring manager / VP-of-Eng audience. |
| Portfolio play | Shipped four single-file AI tools in six weeks — each forkable, BYOK, deployed on GitHub Pages. | LinkedIn launch post. Demonstrates velocity over polish. |

### 6.2 Multiplying the impact across a portfolio

EM Cockpit is the first tool in what should be a 4–6 project series. The same skeleton powers each one — only the prompt and the four output sections change. A suggested sequence:

1. **Week 1 · PR Triage Co-pilot** — paste open-PR list, get review order with risk/impact.
2. **Week 2 · 1:1 Prep Studio** — paste recent notes on one report, get an agenda with growth, blockers, recognition.
3. **Week 3 · Incident Retro Drafter** — paste pager + Slack thread, get a draft RCA with timeline, contributing factors, action items.
4. **Week 4 · EM Cockpit (this project)** — the morning briefing.
5. **Week 5 · Hiring Loop Synth** — paste interviewer notes, get a hire/no-hire summary with calibration flags.
6. **Week 6 · Quarterly Pulse** — paste sprint history, get a quarter-over-quarter team-health report.

Shipping six tools in six weeks does more for an EM's LinkedIn presence than one polished product, because each post is a fresh hook with the same underlying credibility ("this person ships").

---

## 7. Forking the skeleton

To turn EM Cockpit into another tool in the series, three things change. Everything else is reused.

### Change 1 — The prompt persona and JSON shape

Edit `buildPrompt()` in the script block. Replace the persona line and the JSON shape with whatever the new tool returns. For PR Triage, for example, the shape becomes:

```json
{
  "review_order": [{"pr": "#1234 auth-redesign", "owner": "maya", "risk": "high", "reason": "..."}],
  "first_three": ["#1234", "#1240", "#1255"],
  "skip_for_now": [{"pr": "#1199", "reason": "stale, owner OOO"}],
  "summary": "..."
}
```

### Change 2 — The form labels

Five form fields and one notes textarea. Rename them to match the new domain. The `collectInput()` function automatically picks up whatever IDs are present, so no JS changes are needed.

### Change 3 — The four output sections

Inside the result div, rename the four section headers and tweak the `render()` function's four `innerHTML` blocks to match the new JSON keys. Roughly 15 lines change.

Everything else — the provider adapters, the key field, the demo fallback, the design system, the deploy story — is reused as-is. Average fork time is 30 minutes once the first project ships.

---

## 8. Roadmap

- **v1.1** — Persist last input in memory across tab switches (still no localStorage).
- **v1.2** — Export briefing as Markdown to clipboard.
- **v2.0** — Optional GitHub / Linear / on-call connectors via a thin Cloudflare Worker.
- **v2.1** — Diff today's briefing against yesterday's — surface what shifted overnight.
- **v3.0** — Multi-EM mode for skip-level managers viewing 3–5 teams in one pane.

---

*End of document — EM Cockpit v1.0, architecture & impact brief.*
