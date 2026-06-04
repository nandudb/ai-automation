# Posting calendar — AI Automation Series

Six weeks. Eight posts. One launch + one "lesson learned" follow-up per project, plus two narrative pieces (kickoff + finale).

The pattern: **post 1 announces the tool, post 2 (a few days later) shares what you learned from feedback.** The follow-up always out-performs the launch on LinkedIn because by then you have specifics: who used it, what they asked for, what changed.

---

## The 8-post schedule

| # | Date | Topic | Type | Post anchor |
|---|---|---|---|---|
| 0 | Tue 2026-05-19 | **Series kickoff** | Announcement | "Shipping 6 AI tools in 6 weeks. Here's the bet I'm making." |
| 1 | Thu 2026-05-21 | **Week 1: Migration Readiness Pilot** | Launch | Use V1 from `readiness-pilot/LINKEDIN_POST.md` |
| 2 | Tue 2026-05-26 | **Readiness Pilot follow-up** | Lesson | "Three things I learned from the first 48 hours of comments" |
| 3 | Thu 2026-05-28 | **Week 2: EM Cockpit** | Launch | Use V1 from `em-cockpit/LINKEDIN_POST.md` |
| 4 | Tue 2026-06-02 | **EM Cockpit follow-up** | Pattern | "Same skeleton, second tool — here's what's reused and what isn't" |
| 5 | Thu 2026-06-04 | **Week 3: PR Triage Co-pilot** | Launch | (write at week 3 ship) |
| 6 | Thu 2026-06-11 | **Week 4: 1:1 Prep Studio** | Launch | (write at week 4 ship) |
| 7 | Thu 2026-06-18 | **Week 5: Incident Retro Drafter** | Launch | (write at week 5 ship) |
| 8 | Thu 2026-06-25 | **Series finale + Week 6: Hiring Loop Synth** | Wrap | "What I'd do differently if I shipped 6 more" |

**Why this cadence works.** Two posts per project — one to attract a new audience, one to reward the audience that engaged. The Tuesday/Thursday rhythm is when LinkedIn's algorithm pushes professional content hardest in mid-2026. Don't post Monday (everyone's catching up) or Friday (engagement drops).

---

## Post 0 — Series kickoff (write this first)

This is the most important post of the entire series because it sets the frame. Everything after refers back to it.

> I'm running an experiment for the next six weeks.
>
> One AI tool, every Thursday. Same skeleton, different vertical. All single HTML files, all bring-your-own-key, all forkable in 30 seconds.
>
> Week 1: Migration Readiness Pilot — pre-cutover GO/NO-GO healthcheck for cloud migrations.
> Week 2: EM Cockpit — 60-second morning briefing for engineering managers.
> Week 3: PR Triage Co-pilot — review-order optimizer.
> Week 4: 1:1 Prep Studio — agenda generator for direct-report meetings.
> Week 5: Incident Retro Drafter — blameless RCA assistant.
> Week 6: Hiring Loop Synth — calibration helper across interviewer notes.
>
> The bet I'm making: most useful AI tools don't need a backend, an auth system, or a billing layer. They need one focused prompt and a clean output schema. If that's true, six weeks should be enough to prove the pattern across six verticals.
>
> Portfolio + first tool in the comments. Following along publicly — design notes, what worked, what I had to throw out. Comment with the role you'd want me to build a tool for next.
>
> #BuildInPublic #AI #SRE #EngineeringManagement

**Pin the portfolio URL (`nandudb.github.io/ai-automation/`) as the first comment.**

---

## Post 2 — Follow-up template (use this format for every "lesson" post)

After each launch post, wait 4–5 days, then publish a follow-up. The format never changes:

> Three things I learned shipping [Project Name] this week:
>
> 1. [Concrete observation with a number or a verbatim user quote]
> 2. [Design decision you'd make differently — shows growth, not weakness]
> 3. [Surprising piece of feedback — names the kind of person who replied]
>
> What's coming Thursday: [next project teaser in one sentence].
>
> Tool link below.
>
> #BuildInPublic #AI

**Why this format works.** Numbers signal credibility. Naming the kind of person who replied tells the algorithm who to show the post to. Teasing the next project locks in the audience for next week.

---

## Visual asset checklist (per project)

Before each launch post, verify these are live:

- [ ] `og.png` exists (1200×630, used by LinkedIn for the preview card)
- [ ] Static screenshot of the demo output (for the post body — overlays the OG card)
- [ ] Project's `index.html` has correct `og:image` and `og:url` meta tags
- [ ] Portfolio landing page shows the project as **LIVE** (not "DRAFTING")
- [ ] Changelog row has today's date

---

## Engagement plays (the things that compound)

- **Reply to every comment within the first hour.** LinkedIn weights the first-hour engagement window 10× more than later replies.
- **Ask a question in every post.** "What would you score that we're not scoring?" beats "Hope this helps."
- **DM the top 5 commenters from your previous post.** Thank them, tell them what's shipping next, ask if there's a tool they wish existed for their role. About 1 in 3 will reply, and they often turn into beta users for the next project.
- **Quote-share one positive comment per post in your stories or as a follow-up post.** Social proof compounds.
- **At Week 4, write a "halfway" post.** Recap what shipped, what worked, what surprised you. This is where the series goes from "interesting" to "you're someone I should follow."

---

## Hashtag rotation

Don't repeat the same hashtags every week — the algorithm down-weights repetition. Rotate from this pool, 2–3 per post:

`#BuildInPublic` `#AI` `#LLM` `#SRE` `#EngineeringManagement` `#CloudMigration` `#DevTools` `#TechLead` `#ProgramManagement` `#StartupTools` `#ProductEngineering` `#CodeReview` `#Postmortem` `#Hiring`

Pair one broad (#AI, #BuildInPublic) with one specific (#SRE, #EngineeringManagement) per post.

---

## Metrics worth tracking

After each post (24h, 48h, 7d):

- Impressions
- Click-through rate to the portfolio
- Tool's GitHub stars / forks delta
- Comments — categorize as: question, praise, suggestion, request-for-different-vertical

If the **request-for-different-vertical** count exceeds 5 on any post, build that next instead of the planned project. The audience is telling you what they want.

---

## After Week 6

Three options for what's next, in increasing ambition:

1. **Bundle and repackage.** Write a single Medium / dev.to article with all six tools embedded — the "ultimate guide to single-file AI tools." Republished content gets a second wave.
2. **Open the pattern as a starter template.** Strip a tool down to a skeleton repo (`single-file-ai-tool-starter`) and publish it. This earns inbound stars for months.
3. **Build the connector layer.** v2.0 of any of the six tools — add a thin Cloudflare Worker that pulls from one real data source. Becomes the first "non-trivial" project in the portfolio and the natural next series.

Pick option 2 if your goal is reach. Pick option 3 if your goal is interviews.
