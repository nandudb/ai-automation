# EM Cockpit

> Run your engineering week in 60 seconds. Paste your team state — get a focus list, risks to watch, and decisions waiting on you, before standup.

![Status](https://img.shields.io/badge/status-v1.0-7cf7d2)
![Single file](https://img.shields.io/badge/build-none%20%C2%B7%20one%20HTML-9d8cff)
![BYOK](https://img.shields.io/badge/api-BYOK-ffb86b)
![License](https://img.shields.io/badge/license-MIT-8af0a0)

**Live demo:** `https://<your-handle>.github.io/em-cockpit/`

---

## Why this exists

Engineering Managers don't lack information — they drown in it. By the time standup hits, your tabs are open in Linear, GitHub, Slack, the on-call dashboard, your 1:1 doc, and that retro thread from Friday. The first 30 minutes of every day go to *triage*, not *leadership*.

EM Cockpit collapses that triage. You paste what's in flight, an LLM gives you back four things and only four:

- **TODAY'S TOP 3** — the people/shipping actions that actually move the needle.
- **RISKS TO WATCH** — concrete, named, and tied to your input.
- **DECISIONS WAITING ON YOU** — questions only you can call.
- **TEAM HEALTH** — honest 0–100 score with a one-line rationale.

That's it. No dashboards. No second screen.

---

## What it looks like

| Input pane | Output pane |
|---|---|
| Form (reports, meetings, PRs, on-call, notes) OR free-form paste. | Top 3, risks, decisions, health score — rendered in 1–3 seconds. |

The reference design uses a dark "command-center" aesthetic, mono accents, and a single `index.html` you can drop into GitHub Pages.

---

## Quick start

```bash
git clone https://github.com/<you>/em-cockpit.git
cd em-cockpit
open index.html        # macOS
# or: python3 -m http.server 8080 && open http://localhost:8080
```

That's the whole install. There is no build step.

To deploy: enable **GitHub Pages** on the repo (`Settings → Pages → main / root`). Your tool is live at `https://<you>.github.io/em-cockpit/`.

---

## Architecture (in one paragraph)

A single `index.html` with three sections — input form, provider/key picker, output renderer — and a 200-line `<script>` block. On submit, it builds a strict-JSON prompt, dispatches to the selected provider (Groq, OpenAI, or Anthropic) via `fetch()` directly from the browser, parses the response, and renders four DOM regions. Keys never leave the browser. No backend, no telemetry, no build pipeline.

```
┌─────────────────┐      ┌────────────────┐      ┌──────────────────┐
│  Form / Paste   │ ───▶ │  Prompt + Key  │ ───▶ │  Provider API    │
│  (browser DOM)  │      │  (dispatcher)  │      │  (Groq/OAI/Claude)│
└─────────────────┘      └────────────────┘      └────────┬─────────┘
                                                          │ JSON
                                                          ▼
                                                ┌──────────────────┐
                                                │  Render 4 panels │
                                                │  Top3 · Risks ·  │
                                                │  Decisions · Score│
                                                └──────────────────┘
```

### Why this stack

- **Single HTML file** — no toolchain rot, ships on GitHub Pages, forkable in 30 seconds.
- **BYOK (bring your own key)** — no auth, no server, no recurring cost for the maintainer.
- **JSON mode + strict schema** — the model is forced into a structure, so the render code stays simple.
- **Three providers behind one adapter** — readers can ship the model they already pay for.

---

## Customize it

The prompt is the product. It lives in `buildPrompt()` near the top of the `<script>`. Swap the role ("Engineering Manager's chief-of-staff"), the four output sections, the JSON shape — and you have a new tool. The render layer reads whatever fields you ask for.

Forks that take ~15 minutes:

- **PR Triage Co-pilot** — paste your open-PR list, get a review order.
- **1:1 Prep Studio** — paste recent notes about one report, get an agenda.
- **Incident Retro Drafter** — paste pager + Slack thread, get a draft RCA.
- **Hiring Loop Synth** — paste interviewer notes, get a hire/no-hire summary.

---

## Privacy

- Your API key is read from a form field and used in a single `fetch()` to the provider you choose.
- Nothing is sent to any server controlled by this project — there is no such server.
- The tool does not call `localStorage` or `sessionStorage`. Close the tab; the key is gone.

If you're pasting sensitive content (names, internal projects), use a provider whose data-retention terms you're comfortable with.

---

## Impact (how to talk about it on your résumé)

Pick the framing that matches your audience:

- **Time saved:** "Replaced a 25-minute morning triage with a 60-second briefing — 2 hours/week per EM."
- **Decision latency:** "Surfaces stalled decisions by age; pushed median decision age from 4 days to under 2."
- **Onboarding:** "New EMs get a structured first-90 routine on day one, not month three."
- **Portfolio play:** "Shipped four single-file AI tools in six weeks — each forkable, BYOK, deployed on GitHub Pages."

---

## Roadmap

- v1.1 — Save last input to in-memory state across tab switches.
- v1.2 — Export briefing as Markdown (clipboard + download).
- v2.0 — Optional connectors (GitHub PRs, Linear, on-call schedules) via a thin Cloudflare Worker.
- v2.1 — Compare today's briefing to yesterday's — what shifted?

---

## License

MIT. Fork it, rename it, ship your own.
