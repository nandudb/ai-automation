# Migration Readiness Pilot

> Run a cloud-migration readiness check in 60 seconds. Paste your source + target platform state — get a GO / NO-GO verdict, blockers, an 8-dimension scorecard, and a pre-cutover checklist ordered by what'll break first.

![Status](https://img.shields.io/badge/status-v1.0-7cf7d2)
![Single file](https://img.shields.io/badge/build-none%20%C2%B7%20one%20HTML-9d8cff)
![BYOK](https://img.shields.io/badge/api-BYOK-ffb86b)
![License](https://img.shields.io/badge/license-MIT-8af0a0)

**Live demo:** `https://<your-handle>.github.io/migration-readiness-pilot/`

---

## Why this exists

Migration readiness reviews drown in PDFs, Confluence pages, and Excel checklists. By the time the steering committee asks *"are we ready to cut over?"*, the answer is either an evasive "mostly" or a half-day deck-building exercise.

Migration Readiness Pilot collapses that into a 60-second briefing. You paste your source + target state, the model returns four artifacts:

- **VERDICT** — GO, CONDITIONAL GO, or NO-GO, with a confidence %.
- **BLOCKERS** — P0 / P1 / P2, each with category and a concrete remediation.
- **READINESS SCORECARD** — 8 dimensions scored 0–100, with a one-line note each.
- **PRE-CUTOVER CHECKLIST** — 5–8 actions, ordered T-minus days from cutover, with owners.

Designed for engineers, SREs, and program managers running *any* migration — on-prem → cloud, Gen1 → Gen2, region → region, monolith → cells.

---

## The 8 dimensions

Every healthcheck scores these — same eight, every time, so reports are comparable across migrations and across weeks:

1. **Network & Connectivity** — circuits, BGP, DNS cutover, latency budget
2. **Identity & Access (IAM)** — compartments, federation, service principals, secrets
3. **Database & Data** — version compatibility, replication, RPO, schema drift
4. **Compute & Workloads** — shape mapping, OS/runtime versions, autoscale policy
5. **Security & Compliance** — SOC2/PCI scope, vault rotation, vulnerability scan baseline
6. **Observability & Logging** — metrics, traces, log shipping, alert routes
7. **DR & Backup** — failover drill recency, RTO test results, backup integrity
8. **Operational Readiness** — runbooks, rollback playbook, on-call rotation, comms tree

---

## Architecture

Single `index.html`. The architecture in one paragraph: an input form (or paste pane), a provider/key picker (Groq / OpenAI / Anthropic), a prompt builder that forces strict-JSON output, three async adapters behind one dispatcher map, and a 70-line renderer that paints four DOM regions — verdict banner, blocker cards, scorecard bars, and a clickable checklist. Keys never leave the browser. No backend, no telemetry, no build pipeline.

```
┌─────────────────┐      ┌────────────────┐      ┌──────────────────┐
│  Form / Paste   │ ───▶ │  Prompt + Key  │ ───▶ │  Provider API    │
│  (browser DOM)  │      │  (dispatcher)  │      │  (Groq/OAI/Claude)│
└─────────────────┘      └────────────────┘      └────────┬─────────┘
                                                          │ JSON
                                                          ▼
                                ┌────────────────────────────────────┐
                                │  render() → 4 regions               │
                                │  Verdict · Blockers · Scorecard ·   │
                                │  Pre-cutover Checklist              │
                                └────────────────────────────────────┘
```

### Why this stack

- **Single HTML file** — no toolchain rot, ships on GitHub Pages, forkable in 30 seconds.
- **BYOK** — no auth, no backend, no maintainer billing.
- **JSON mode + strict schema** — model is forced into structure; render code stays simple.
- **Three providers behind one adapter** — readers ship on the model they already pay for.
- **Verdict logic encoded in the prompt** — GO requires zero P0 and no dimension <60; the model can't quietly hand-wave a green light.

---

## Quick start

```bash
git clone https://github.com/<you>/migration-readiness-pilot.git
cd migration-readiness-pilot
open index.html        # macOS
# or: python3 -m http.server 8080 && open http://localhost:8080
```

No build step. To deploy: enable **GitHub Pages** (`Settings → Pages → main / root`) — live at `https://<you>.github.io/migration-readiness-pilot/`.

---

## How to use it

1. Fill the **form** (source, target, scope, SLOs, team, known risks, free-form notes) — *or* drop a runbook/architecture-doc/jira-export into the **Paste** tab.
2. Pick a provider and paste an API key (or skip and use **Try Demo** to see the output).
3. Hit **Run Healthcheck**. Verdict in 1–3 seconds.
4. Click items in the checklist to strike them through (in-memory only — no storage).
5. **Copy as Markdown** to drop the full report into Confluence, Slack, or a ticket.

---

## Customize it

The prompt is the product. It lives in `buildPrompt()`. Swap the persona, the JSON shape, the verdict logic, or the 8 dimensions — and you have a new tool. The render layer reads whatever fields you ask for.

Quick forks (~15 minutes each):

- **DR Readiness Pilot** — same skeleton, scored against an RTO/RPO target.
- **SOC2 Audit Pre-Check** — control-mapped scorecard, evidence-gap blockers.
- **Service Launch Readiness** — production-launch checklist (DRT pattern from Google's SRE book).
- **Vendor Onboarding HealthCheck** — security, contracts, integration, ops.

---

## Privacy

- API key is read from a form field and used in a single `fetch()` to the provider you choose.
- Nothing is sent to any server controlled by this project — there is no such server.
- The tool does not call `localStorage` or `sessionStorage`. Close the tab; the key is gone.
- If your migration state contains sensitive details (customer names, internal project codenames, IPs), use a provider whose data-retention policy you're comfortable with.

---

## Impact (résumé / LinkedIn framing)

Pick the angle that matches your audience:

- **Time saved:** "Replaced a half-day readiness-review prep with a 60-second AI briefing."
- **Decision quality:** "8-dimension scorecard cut go/no-go meetings from 45 minutes to 12."
- **Repeatability:** "Standardized readiness format across 12 migration projects — first apples-to-apples comparison the org has ever had."
- **Portfolio play:** "Second of six single-file AI tools — same skeleton, swap the prompt, ship in a day."

---

## Roadmap

- v1.1 — Save last report as `.md` download (not just clipboard).
- v1.2 — Compare two reports side-by-side ("how did we do vs. last week?").
- v2.0 — Optional GitHub / Confluence / Jira connectors via Cloudflare Worker.
- v2.1 — Custom 8-dimension definitions per org (read from a YAML config).

---

## License

MIT. Fork it, rename it, retune the dimensions, ship your own.
