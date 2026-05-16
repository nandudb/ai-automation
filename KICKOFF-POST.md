# Kickoff post — Week 1 + series announcement

One post that does both: kicks off the six-week series AND launches Week 1 (Migration Readiness Pilot). Three versions below. Pick the one whose tone matches the day.

---

## Version 1 — Recommended (hook → tool → design trick → series)

> The first 30 minutes of every cloud migration "are we ready?" meeting are spent assembling the same Confluence page everyone already had open.
>
> This week I shipped a tool that replaces those 30 minutes with 60 seconds.
>
> It's also the first of six.
>
> → Migration Readiness Pilot
> Paste your source + target state. Get back a verdict (GO / CONDITIONAL GO / NO-GO) with a confidence %, blockers ranked P0 / P1 / P2 with one-step remediations, an 8-dimension readiness scorecard (Network, IAM, Database, Compute, Security, Observability, DR/Backup, Operations), and a T-minus pre-cutover checklist.
>
> One HTML file. Bring your own API key — Groq's free tier works fine. No backend. Open source.
>
> The design choice worth talking about: the verdict logic lives in the prompt, not the code. GO only fires if there are zero P0 blockers AND no scorecard dimension below 60. The model has to defend a green call against the math — it can't quietly hand-wave a green light.
>
> This is Week 1 of a six-week series. Same skeleton, different vertical, one new tool every Thursday:
>
> Week 1 → Migration Readiness Pilot (today)
> Week 2 → EM Cockpit (engineering manager morning briefing)
> Week 3 → PR Triage Co-pilot
> Week 4 → 1:1 Prep Studio
> Week 5 → Incident Retro Drafter
> Week 6 → Hiring Loop Synth
>
> The bet I'm making: most useful AI tools don't need a backend, an auth system, or a billing layer. They need one focused prompt and a clean output schema.
>
> Tool + full portfolio link in the first comment. If you've run a migration recently — what's the dimension you'd score that I'm not?
>
> #CloudMigration #BuildInPublic #AI

---

## Version 2 — Manifesto tone (the bet first)

> I'm running an experiment.
>
> For the next six weeks I'm shipping one AI tool every Thursday. Same skeleton, different vertical, all single HTML files, all bring-your-own-key, all forkable in 30 seconds.
>
> The bet: most useful AI tools don't need a backend, an auth system, or a billing layer. They need one focused prompt and a clean output schema. Six weeks should be enough to prove the pattern across six verticals.
>
> Week 1 ships today.
>
> → Migration Readiness Pilot
> A pre-cutover healthcheck for cloud migrations. Paste your source + target state. Get back a verdict (GO / CONDITIONAL / NO-GO), ranked blockers, an 8-dimension readiness scorecard, and a T-minus checklist. 60 seconds.
>
> The interesting design call: the verdict logic is encoded in natural language inside the prompt — GO only if zero P0s and no dimension below 60. The model has to defend a green call against the math; it can't just default to optimism.
>
> Coming up:
> Week 2 — EM Cockpit (engineering manager morning briefing)
> Week 3 — PR Triage Co-pilot
> Week 4 — 1:1 Prep Studio
> Week 5 — Incident Retro Drafter
> Week 6 — Hiring Loop Synth
>
> Tool + portfolio in the first comment. Building in public — I'll post design notes, what worked, what I threw out.
>
> Comment with the role you'd want me to build a tool for next.
>
> #BuildInPublic #AI #CloudMigration

---

## Version 3 — Story-led (specific scene, then pivot)

> Last quarter I sat through a migration readiness review that lasted four hours.
>
> Three of those hours were assembly — someone screen-sharing Confluence, someone else exporting Jira, a third person re-counting open PRs. The remaining hour was the actual conversation: should we go on schedule, slip, or split the phases?
>
> This week I built the tool I wished we'd had.
>
> → Migration Readiness Pilot
> Paste your source + target state. Get back in 60 seconds:
>
> → a GO / CONDITIONAL GO / NO-GO verdict with confidence %
> → blockers ranked P0 / P1 / P2 with one-step remediations
> → an 8-dimension readiness scorecard (Network, IAM, DB, Compute, Security, Observability, DR, Ops)
> → a T-minus pre-cutover checklist
>
> Single HTML file. Bring your own API key — Groq's free tier works. No backend. Open source.
>
> What makes the output honest: the verdict logic is encoded in the prompt itself. GO only fires when there are zero P0 blockers AND no scorecard dimension below 60. The model can't quietly hand-wave a green light.
>
> This is the first of six. Each Thursday for the next six weeks I'm shipping one tool that solves one job for one role — EMs, SREs, program managers. Same skeleton, swap the prompt.
>
> Tool + the full portfolio in the first comment. If you've run a migration recently, what dimension would you add to the scorecard?
>
> #CloudMigration #BuildInPublic #SRE

---

## Publish-day checklist

- [ ] Push the repo and run all three URLs through the [LinkedIn Post Inspector](https://www.linkedin.com/post-inspector/) (forces fresh OG cache)
- [ ] Publish the post between Tue–Thu, 8:30–10am local time
- [ ] Pin `https://nandudb.github.io/ai-automation/` as the first comment
- [ ] Reply to every comment in the first hour (algorithm weights this 10×)
- [ ] DM the top 5 commenters within 24h — thank them, tell them what ships next Thursday, ask what tool they wish existed for their role
- [ ] 4–5 days later: publish the follow-up "Three things I learned from the first 48h of comments"

## Why these openings work

- **V1's opener** ("first 30 minutes ... assembling the same Confluence page everyone already had open") is recognizable to anyone who's run a migration — it's a fact, not an opinion. Facts open better than opinions.
- **V2's opener** ("I'm running an experiment") signals you're inviting the reader to watch a story unfold, not just buy a tool. Works well if you have an existing audience.
- **V3's opener** (specific 4-hour meeting) is the most cinematic and the most "human" — it works best if you want to be perceived as a practitioner first, builder second.

All three end with a question, which is what compounds comments — and comments are what compound reach.
