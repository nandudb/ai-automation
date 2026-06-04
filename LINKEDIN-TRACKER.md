# LinkedIn Posts Tracker · AI Automation Series

Single source of truth for every LinkedIn post in the AI Automation Portfolio series. Drafts, schedule, metrics, learnings — all here.

**Series:** AI Automation — Six tools, six weeks
**Started:** _fill in when Post 0 publishes_
**Author:** [Nanda T](https://linkedin.com/in/nandat) · [GitHub](https://github.com/nandudb)
**Portfolio URL:** https://nandudb.github.io/ai-automation/

---

## How to use this page in Notion

1. In Notion, open a new page → click the `···` menu → **Import** → **Markdown & CSV** → select this file.
2. Notion will import each table as an inline table. To convert any table into a full database with filters/views, click the `···` next to the table header → **Turn into database**.
3. Each "Post N" section below is designed to become its own sub-page once you split them up. Right-click the heading → **Turn into page**.
4. Update the **Posts Master Table** as the source of truth. The per-post sections hold the drafts, copy, and learnings.

---

## At-a-glance dashboard

| Metric | Value |
|---|---|
| Current week | Week 1 |
| Posts shipped | 0 / 8 |
| Total impressions (lifetime) | 0 |
| Total clicks to portfolio | 0 |
| Total new followers | 0 |
| Next post due | _fill in_ |
| Next post project | Migration Readiness Pilot |

---

## Posts master table

| # | Status | Type | Project | Target date | Posted on | Hook (first line) | Impressions | Reactions | Comments | Reposts | CTA clicks | Followers gained | Post URL |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | Draft | Kickoff + Launch | Migration Readiness Pilot | _fill in_ | — | Have you ever sat through a four-hour cloud migration readiness meeting... | — | — | — | — | — | — | — |
| 1 | Planned | Follow-up | Migration Readiness Pilot | Post 0 + 4 days | — | Three things I learned from the first 48 hours... | — | — | — | — | — | — | — |
| 2 | Planned | Launch | EM Cockpit | Post 1 + 3 days | — | The first 25 minutes of every Engineering Manager's day... | — | — | — | — | — | — | — |
| 3 | Planned | Follow-up | EM Cockpit | Post 2 + 4 days | — | Same skeleton, second tool — here's what's reused... | — | — | — | — | — | — | — |
| 4 | Planned | Launch | PR Triage Co-pilot | Post 3 + 3 days | — | _to draft_ | — | — | — | — | — | — | — |
| 5 | Planned | Launch | 1:1 Prep Studio | Post 4 + 7 days | — | _to draft_ | — | — | — | — | — | — | — |
| 6 | Planned | Launch | Incident Retro Drafter | Post 5 + 7 days | — | _to draft_ | — | — | — | — | — | — | — |
| 7 | Planned | Series wrap | Hiring Loop Synth | Post 6 + 7 days | — | What I'd do differently if I shipped 6 more... | — | — | — | — | — | — | — |

**Status legend:** `Draft` · `Approved` · `Scheduled` · `Published` · `Iterating` · `Archived`
**Type legend:** `Kickoff` · `Launch` · `Follow-up` · `Series wrap` · `Off-cadence`

---

## Post 0 · Kickoff + Week 1 launch (Migration Readiness Pilot)

### Pre-publish checklist

- [ ] Final copy approved (under 3,000 chars)
- [ ] OG card verified at https://www.linkedin.com/post-inspector/
- [ ] All three URLs load in incognito browser
- [ ] First-comment text copied to clipboard
- [ ] One screenshot of the demo output saved (for inline image)
- [ ] Calendar reminder set for first-hour reply window
- [ ] Calendar reminder set for follow-up post (Post 1)

### Final copy

```
🪝 Have you ever sat through a four-hour cloud migration readiness meeting just to leave with "we'll know more next week"?

I have. More times than I should admit.

🩺 Why every readiness review dies the same way.

Thirty minutes burned screen-sharing the same Confluence page everyone already had open. Another hour on status-by-name-around-the-room. By the time someone asks the real question — go, slip, or split? — the energy is gone. The answer is always "let's reconvene Friday."

🛠 So this week I rebuilt the meeting.

Migration Readiness Pilot. Paste your source and target state. 60 seconds later, four outputs:

A verdict (GO / CONDITIONAL GO / NO-GO) with confidence %
Blockers ranked P0/P1/P2 with one-step remediations and owners
An 8-dimension readiness scorecard — Network, IAM, Database, Compute, Security, Observability, DR/Backup, Operations — same eight every time, so migrations are finally comparable
A T-minus pre-cutover checklist

⚙ How it works under the hood.

One HTML file. No backend, no login, no telemetry. Bring your own API key — Groq's free tier is enough. The model is locked into a strict JSON schema.

The design call I keep coming back to: the verdict logic lives in the prompt, not the code. GO only fires if there are zero P0 blockers AND no dimension below 60. Models default to optimism. Putting the math in plain English forces honesty.

📋 What it looks like in practice.

A team moving from on-prem Oracle 12c to ExaCC X9M pasted in: source version, target shape, FastConnect status, DR drill recency (24 months stale — yes, really), IAM progress (not started), one vendor library without a Gen2 driver. Result: CONDITIONAL GO at 72%. Two P0s, both fixable in eleven days. A checklist that said the DR drill had to happen by T-7, not "soon." That alone reframed the week.

💬 What would you score that I'm not?

Building in public, so feedback shapes what ships next. If you've been in one of those meetings — what's the dimension you'd add or drop? Drop a line in the comments. I read everything.

👀 What if every engineering manager started their morning the same way?

This is the first of six tools. Same skeleton, different vertical, one new tool every Thursday:

Week 1 → Migration Readiness Pilot (today)
Week 2 → EM Cockpit · engineering manager morning briefing
Week 3 → PR Triage Co-pilot
Week 4 → 1:1 Prep Studio
Week 5 → Incident Retro Drafter
Week 6 → Hiring Loop Synth

Next Thursday: Week 2 — what actually makes a briefing useful, versus just a list of facts?

Live tool, portfolio, and source in the first comment.

#CloudMigration #BuildInPublic #AI
```

### First comment

```
Live tool: https://nandudb.github.io/ai-automation/readiness-pilot/

Full portfolio (all six tools): https://nandudb.github.io/ai-automation/

Source on GitHub: https://github.com/nandudb/ai-automation
```

### Metrics snapshots

| Window | Impressions | Reactions | Comments | Reposts | CTA clicks | Followers gained | Profile views |
|---|---|---|---|---|---|---|---|
| 1 hour | — | — | — | — | — | — | — |
| 24 hours | — | — | — | — | — | — | — |
| 48 hours | — | — | — | — | — | — | — |
| 7 days | — | — | — | — | — | — | — |
| 30 days | — | — | — | — | — | — | — |

### Top engagement (fill in as comments arrive)

| Commenter | Role | Comment / question | My reply | Action taken |
|---|---|---|---|---|
|  |  |  |  |  |

### Learnings log

- **What worked:** _fill in after 48h_
- **What surprised me:** _fill in_
- **What I'd change next time:** _fill in_
- **What I'll keep in the playbook:** _fill in_

---

## Post 1 · Readiness Pilot follow-up (Three things I learned)

### Pre-publish checklist

- [ ] Wait 4–5 days after Post 0
- [ ] Have at least one screenshot or quote from a real comment
- [ ] Have one concrete number ("X clones / Y comments / Z reach")
- [ ] Final copy under 3,000 chars
- [ ] First comment prepped

### Template (fill in with real data after Post 0 publishes)

```
Three things I learned shipping Migration Readiness Pilot this week:

1. [Concrete observation with a number — e.g., "The dimension everyone asked for was Cost — I'd missed it. Added in v1.1."]

2. [Design decision I'd make differently — e.g., "The 8-dimension scorecard is too dense for the OG card preview. Next launch I'll show 4 dimensions on the card and let the rest reveal in the tool."]

3. [Surprising piece of feedback — e.g., "Half the comments were from program managers, not SREs. The tool is more useful for non-technical stakeholders running readiness reviews than for engineers building them."]

What's coming Thursday: a 60-second morning briefing tool for engineering managers. The harder design problem there: what separates a useful briefing from a list of facts?

Tool link below.

#BuildInPublic #AI
```

### Metrics snapshots

| Window | Impressions | Reactions | Comments | Clicks |
|---|---|---|---|---|
| 24 hours |  |  |  |  |
| 7 days |  |  |  |  |

---

## Post 2 · EM Cockpit launch

### Pre-publish checklist

- [x] Build OG card variant for EM Cockpit (`em-cockpit/og.png` — already shipped)
- [ ] Verify EM Cockpit page in Post Inspector
- [ ] Wait at least 4 days after Post 0 to maintain cadence
- [ ] Confirm Post 1 (Readiness Pilot follow-up) is also out
- [ ] Final copy under 3,000 chars
- [ ] First comment prepped

### Final copy (paste-ready, emoji-anchored)

```
🪝 I had 17 tabs open before standup yesterday.

None of them helped me decide anything.

🩺 Every EM has the same morning routine.

Linear for sprint status. GitHub for PR backlog. Slack for overnight escalations. On-call for what fired. 1:1 notes for follow-ups. By the time standup hits, the freshest 25 minutes are gone and you've assembled context, not made a single decision.

🛠 So I rebuilt the morning.

EM Cockpit. Paste your team state — sprints, on-call, open PRs, decisions waiting, 1:1 follow-ups — and 60 seconds later, four outputs:

Today's top 3 — people and shipping actions, not status to read
Risks to watch — concrete, named, tied to your input
Decisions waiting on you, with age in days
A team-health score with a one-line rationale

⚙ How it works under the hood.

Same skeleton as last week's Readiness Pilot. One HTML file, no backend. Bring your own API key — Groq's free tier is enough. Strict JSON output.

The design call worth talking about: the Top 3 must be ACTIONS, not facts. Left to its preferences, the model writes "Status of PR backlog is X." Useless. The prompt has one negative rule — "lead with a verb. Top 3 are PEOPLE or SHIPPING actions, not info to read." That single line turns a briefing into a decision aid.

📋 What it looks like in practice.

An EM with 6 engineers pastes in: 14 open PRs (4 stale), one new-hire PR open day 9, two overnight incidents, Priya asking about her promo packet, Maya blocked on auth-redesign scope.

Top 3: Unblock Maya before 11. Greenlight observability vendor by Friday. 1:1 with Priya — bring last quarter's impact doc.
Risks: schema migration slipping, Jamal's fourth straight week on-call, new-hire PR open day 9.
Decisions waiting: auth-redesign (4d), observability vendor (2d), Q3 headcount (6d).
Health: 74 · STEADY. Velocity flat. On-call load elevated. PR backlog is the leading indicator.

The EM walked into standup having decided the day, not assembled it.

💬 What's the first thing you check?

If you're an EM with a morning routine that works, I'd love to hear it. What do you open first? What did you cut? Drop a line — I read everything.

👀 What if review order weighed the new hire's PR as much as the staff engineer's?

This is Week 2 of six tools. Same skeleton, swap the prompt, ship in a day:

Week 1 → Migration Readiness Pilot
Week 2 → EM Cockpit (today)
Week 3 → PR Triage Co-pilot
Week 4 → 1:1 Prep Studio
Week 5 → Incident Retro Drafter
Week 6 → Hiring Loop Synth

Next Thursday: PR Triage. The question I'm chewing on — should review order weigh blast radius (size of change) or author tenure (newer authors need more support)? Curious where you'd land.

Live tool, portfolio, and source in the first comment.

#EngineeringManagement #BuildInPublic #AI
```

### First comment

```
Live tool: https://nandudb.github.io/ai-automation/em-cockpit/

Last week's tool (Migration Readiness Pilot): https://nandudb.github.io/ai-automation/readiness-pilot/

Full portfolio (all six tools): https://nandudb.github.io/ai-automation/

Source on GitHub: https://github.com/nandudb/ai-automation
```

### Section map (verify all 7 sections landed)

| # | Tag | Heading | Type |
|---|---|---|---|
| 1 | Hook | *How many tabs do you have open before standup...* | Question |
| 2 | The pain | *Every EM has the same morning routine.* | Statement |
| 3 | The change | *So I rebuilt the morning.* | Statement |
| 4 | The mechanism | *How it works under the hood.* | Statement |
| 5 | The example | *What it looks like in practice.* | Statement |
| 6 | The invitation | *What's the first thing you check?* | Question |
| 7 | The tease | *What if review order weighed the new hire's PR as much as the staff engineer's?* | Question |

### Metrics snapshots

| Window | Impressions | Reactions | Comments | Reposts | CTA clicks | Followers gained | Profile views |
|---|---|---|---|---|---|---|---|
| 1 hour |  |  |  |  |  |  |  |
| 24 hours |  |  |  |  |  |  |  |
| 48 hours |  |  |  |  |  |  |  |
| 7 days |  |  |  |  |  |  |  |
| 30 days |  |  |  |  |  |  |  |

### Top engagement

| Commenter | Role | Comment / question | My reply | Action taken |
|---|---|---|---|---|
|  |  |  |  |  |

### Learnings log

- **What worked:** _fill in_
- **What surprised me:** _fill in_
- **What I'd change:** _fill in_

---

## Post 3 · EM Cockpit follow-up (Same skeleton, second tool)

### Hook angle
This is the post that proves the *pattern*, not the tool. Talks about reuse, what changed, what stayed the same.

### Draft (to write)

```
[Draft will go here]
```

---

## Post 4 · PR Triage Co-pilot launch

### Pre-publish checklist

- [x] Ship PR Triage tool — `pr-triage/index.html`
- [x] Build OG card — `pr-triage/og.png` (1200×630)
- [x] Update portfolio landing to mark Week 3 LIVE
- [ ] Push to GitHub
- [ ] Verify URL in Post Inspector
- [ ] Confirm at least 4 days have passed since Post 2 (EM Cockpit)
- [ ] First comment prepped

### Final copy (paste-ready, emoji-anchored)

```
🪝 There are 14 open PRs in my review queue this morning. Four are stale. One is a new hire waiting nine days for feedback on their first PR.

🩺 Most EMs review PRs in the wrong order.

Newest first. Biggest first. Loudest-in-Slack first. None of those weight what actually matters: a PR sitting in a new hire's queue for nine days isn't just slow — it's a ramp signal that compounds. Your slowest developer this morning is whoever you're not reviewing.

🛠 So I built the tool that ranks them honestly.

PR Triage Co-pilot. Paste your backlog — counts, authors, sizes, ages — and 30 seconds later, four outputs:

A one-line backlog summary
The first three to review NOW
A full ranked review order with size badges (S/M/L/XL)
A skip-for-now list with reasons

⚙ How it works under the hood.

Same skeleton as the last two tools. One HTML file, no backend. BYOK. Strict JSON output.

The design call worth talking about: review order isn't a function of size. It's impact × urgency × ramp signals. The prompt has one negative rule that does the real work — "new-hire PRs open >3 days get a +1 priority bump. Ramp signals matter more than line count." That single line means a 200-line PR from a new hire ranks above a 2000-line PR from a staff engineer who can update reviewers themselves.

📋 What it looks like in practice.

A tech lead pastes in: 14 open PRs, one critical hotfix, an XL auth-redesign from Maya (staff), a typo fix from Jamal, a new-hire script from Sam (open day 9), a stale dashboard cleanup, and a Friday yak-shave from a dev who's OOO from Wed.

First three: #1262 hotfix (critical, unblocks rollout), #1240 typo (2-minute win, clears the queue), #1255 Sam's PR (+1 ramp bump — beats every bigger PR in the queue).
Then Maya's XL auth-redesign at #4 — important, but Maya can update reviewers. Sam can't.
Skip: the Friday yak-shave. Author OOO from Wed. Reviewing today wastes the round-trip.

The tech lead reviewed the right three in 12 minutes instead of 60.

💬 What's your PR triage rule?

If you've got a heuristic that works — a Friday review afternoon, a "skip your own team" rule, a max-3-deep-reviews-a-day cap — I want to hear it. Drop a line. Same as the last two posts, I read everything.

👀 What does specific recognition sound like when the model has no memory?

This is Week 3 of six tools. Same skeleton, swap the prompt, ship in a day:

Week 1 → Migration Readiness Pilot
Week 2 → EM Cockpit
Week 3 → PR Triage Co-pilot (today)
Week 4 → 1:1 Prep Studio
Week 5 → Incident Retro Drafter
Week 6 → Hiring Loop Synth

Next Thursday: 1:1 Prep Studio. The design problem — how do you make recognition feel specific and non-generic when you're handing the model a paragraph of notes and asking it to call out something meaningful?

Live tool, portfolio, and source in the first comment.

#CodeReview #BuildInPublic #AI
```

### First comment

```
Live tool: https://nandudb.github.io/ai-automation/pr-triage/

Last two tools:
· Migration Readiness Pilot: https://nandudb.github.io/ai-automation/readiness-pilot/
· EM Cockpit: https://nandudb.github.io/ai-automation/em-cockpit/

Full portfolio (all six tools): https://nandudb.github.io/ai-automation/

Source on GitHub: https://github.com/nandudb/ai-automation
```

### Section map (verify all 7 sections landed)

| # | Tag | Heading | Type |
|---|---|---|---|
| 1 | Hook | *14 open PRs · 4 stale · new hire waiting 9 days for feedback on first PR* | Statement (visceral fact) |
| 2 | The pain | *Most EMs review PRs in the wrong order.* | Statement |
| 3 | The change | *So I built the tool that ranks them honestly.* | Statement |
| 4 | The mechanism | *How it works under the hood.* | Statement |
| 5 | The example | *What it looks like in practice.* | Statement |
| 6 | The invitation | *What's your PR triage rule?* | Question |
| 7 | The tease | *What does specific recognition sound like when the model has no memory?* | Question |

### Metrics snapshots

| Window | Impressions | Reactions | Comments | Reposts | CTA clicks | Followers gained | Profile views |
|---|---|---|---|---|---|---|---|
| 1 hour |  |  |  |  |  |  |  |
| 24 hours |  |  |  |  |  |  |  |
| 48 hours |  |  |  |  |  |  |  |
| 7 days |  |  |  |  |  |  |  |
| 30 days |  |  |  |  |  |  |  |

### Top engagement

| Commenter | Role | Comment / question | My reply | Action taken |
|---|---|---|---|---|
|  |  |  |  |  |

### Learnings log

- **What worked:** _fill in_
- **What surprised me:** _fill in_
- **What I'd change:** _fill in_

---

## Post 5 · 1:1 Prep Studio launch

### Draft (to write)

```
[Draft will go here]
```

---

## Post 6 · Incident Retro Drafter launch

### Draft (to write)

```
[Draft will go here]
```

---

## Post 7 · Series wrap + Hiring Loop Synth

### Hook angle
Reflect on what shipped, what worked, what surprised me. End with "what's next" (Series 2 tease or a starter-template offering).

### Draft (to write)

```
[Draft will go here]
```

---

## Hooks pool (reusable openers)

Save here whenever I see a hook I like, or come up with one mid-thought.

### Question-style
- *Have you ever sat through a four-hour [type] meeting just to leave with "we'll know more next week"?*
- *How many [activity] hours did you spend this week that produced an actual decision?*
- *When was the last time a [meeting type] actually told you something you didn't already know?*
- *What if every [role] started their morning with a 60-second briefing instead of 30 minutes of triage?*

### Statement-style
- *Most [thing X] don't fail because of [common explanation]. They fail because nobody knows what "[critical word]" actually means.*
- *The first 30 minutes of every [recurring event] are spent assembling the same [artifact] everyone already had open.*
- *I noticed something embarrassing about my [workflow].*
- *Most [tool category] fail for the same reason: they ask you to check another dashboard.*

### Story-style
- *Last quarter I sat through a [meeting] that lasted four hours. Three of those hours were assembly.*
- *I shipped a tool this week, but the tool is actually the second-most interesting thing about it.*

---

## Hashtag pool

Rotate; max 3 per post. Pair one broad with one specific.

| Broad | Role-specific | Domain |
|---|---|---|
| #BuildInPublic | #SRE | #CloudMigration |
| #AI | #EngineeringManagement | #CodeReview |
| #LLM | #TechLead | #Postmortem |
| #StartupTools | #ProgramManagement | #Hiring |
| #ProductEngineering | #DevTools | #DBAdmin |

---

## First-comment templates

### Standard launch (3 links)

```
Live tool: [URL]

Full portfolio (all six tools): https://nandudb.github.io/ai-automation/

Source on GitHub: https://github.com/nandudb/ai-automation
```

### Follow-up post (1 link back to original)

```
The original post: [URL]
Tool: [URL]
```

### Conversation-starter (link + question)

```
[URL]

Quick question for anyone who clicks: which dimension would you swap out of the scorecard?
```

---

## Engagement playbook

### First hour (the highest-leverage 60 minutes)

- Reply to **every** comment, even one-word ones.
- Use the commenter's first name in the reply.
- End every reply with a follow-up question. Thread depth boosts the algorithm signal more than reply count.
- Don't reply with only emojis. The algorithm reads emoji-only replies as low-effort and weights them down.

### First 24 hours

- DM the top 5 commenters: short, personal, mention what ships next, ask one question.
- Save screenshots of the best comments — they'll feed the follow-up post.
- Quote-share one positive comment as a standalone post if it sparks more discussion.

### Days 3–7

- Add an **"Update:"** edit to the original post with a number ("400 clones · added Cost dimension based on feedback"). Edits trigger a small re-distribution.
- Draft and publish the follow-up "lessons learned" post.

---

## Series-wide learnings log

Append observations as the series progresses.

| Week | Date | Observation | Action / change |
|---|---|---|---|
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

---

## Constants (reference)

| Variable | Value |
|---|---|
| Series name | AI Automation — Six tools, six weeks |
| Total weeks | 6 |
| Cadence | Launch every Thursday + follow-up every Monday/Tuesday |
| Portfolio URL | https://nandudb.github.io/ai-automation/ |
| LinkedIn profile | linkedin.com/in/nandat |
| GitHub repo | github.com/nandudb/ai-automation |
| OG card spec | 1200×630 PNG, dark theme, mint+violet accent |
| Character limit | 3,000 (LinkedIn) |
| Optimal post time (audience tz) | Tue–Thu, 7:30 PM IST / 10:00 AM ET |

---

## Future series ideas (post-Week 6)

Capture ideas here; pick one to commit to in the Week 7 retrospective post.

- **Series 2 — Add a connector layer.** v2.0 of each Week 1–6 tool, each with one real data source (GitHub PRs, Linear issues, on-call API). Proves the pattern scales past BYOK.
- **Series 3 — The skeleton itself.** Publish a starter template repo (`single-file-ai-tool-starter`) and a teaching post that walks through the 200-line skeleton.
- **Series 4 — Tool teardown series.** Pick popular AI tools and analyze what works / what doesn't from an architecture lens.
- **Series 5 — Cross-tool patterns.** Which design patterns held across all six tools? Which ones I had to discard?

---

_Last updated: see file modification date._
