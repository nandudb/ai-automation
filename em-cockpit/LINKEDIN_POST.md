# LinkedIn post — EM Cockpit launch

Three versions below — pick the one that matches the tone you want.
All three are ready to paste. The post-mortem on what makes each one work is at the bottom.

---

## Version 1 — "I built a thing" (Recommended)

> The first 25 minutes of every Engineering Manager's day go to triage, not leadership.
>
> Slack, Linear, on-call, the 1:1 doc, that retro thread from Friday — all open before standup.
>
> So I built a 60-second alternative.
>
> **EM Cockpit** is a single HTML page. You paste what's in flight — sprints, PRs, on-call, decisions waiting — and it returns four things and only four:
>
> → Today's top 3 (people / shipping actions, not info to read)
> → Risks to watch (concrete, named, tied to your input)
> → Decisions waiting on you (with age, in days)
> → Team health score (0–100, with a one-line rationale)
>
> No backend. No login. Bring your own API key (Groq free tier works fine). Drop the file on GitHub Pages and you're live.
>
> The interesting part isn't the code — it's the prompt. The model is forced into a strict JSON schema, which means the render layer stays trivial and the *output never drifts*. Same shape, every morning.
>
> Forking this into a PR-triage tool, a 1:1 prep coach, or an incident-retro drafter is ~15 minutes of work. Same skeleton, swap the prompt.
>
> Repo + live demo in the comments. Would love feedback from other EMs on what you'd add to the briefing.
>
> #EngineeringManagement #AI #BuildInPublic #LLM

---

## Version 2 — "Lesson learned" (more reflective)

> I noticed something embarrassing about my mornings.
>
> Every day, before I led anyone, I spent 25 minutes triaging — flipping between Slack, Linear, on-call, GitHub, my 1:1 notes. By the time standup hit, I'd already burned the freshest part of my brain on context-switching.
>
> So I asked: what if the briefing was the product, not the search?
>
> Built **EM Cockpit** this weekend. One HTML file. You paste your team state, an LLM gives you back: today's top 3 actions, the risks worth chasing, the decisions blocked on you, and a team-health score.
>
> Three things I learned:
>
> 1. **Strict JSON output beats prompt engineering tricks.** Forcing the model into a fixed schema killed 90% of the "creative" failures.
> 2. **BYOK is freedom.** No backend = no recurring cost = no abandoned project in six months.
> 3. **The prompt is the product.** Swap it and you have a PR-triage tool, a 1:1 prep coach, or a retro drafter. Same skeleton.
>
> Repo + demo in the comments. If you're an EM, I'd love to know what you'd add.
>
> #EngineeringManagement #AI #BuildInPublic

---

## Version 3 — "Sharp hook" (highest scroll-stop)

> Most EM productivity tools fail for the same reason: they ask you to *check another dashboard*.
>
> The dashboard isn't the problem. The triage is.
>
> So I built a 60-second briefing instead. Paste your team state → get top 3 actions, risks, blocked decisions, and a health score. One screen. No login.
>
> Three providers behind one adapter (Groq / OpenAI / Claude). One HTML file. Deployable on GitHub Pages in five minutes.
>
> The interesting design choice: forcing the model into a strict JSON schema. The render code stays 40 lines because the output shape never drifts.
>
> Repo + demo below. What would you add to the briefing if it were yours?
>
> #EngineeringManagement #AI #LLM

---

## Posting checklist

- [ ] Pin the repo link as the first comment (LinkedIn's algorithm punishes external links in the post body).
- [ ] Add 1 screenshot of the dark UI showing real output. Static screenshots out-perform GIFs.
- [ ] Post between Tuesday and Thursday, 8:30–10am local time.
- [ ] Reply to the first 5 comments within an hour — engagement window matters.
- [ ] After 48h, edit the post to add a "**Update:**" line with a stat ("400+ devs cloned it" / "added Groq support based on feedback").

## Why these posts work (the structural notes)

- **Opening line is a fact, not an opinion** — "25 minutes triaging" is checkable; "EMs are overwhelmed" is filler.
- **Specific arrows, not bullets** — `→` reads as a list without LinkedIn's bullet formatting (which is ugly in their composer).
- **Three numbered lessons, not five** — three is the magic number for retention on the platform.
- **One question at the end** — invites comments, which the algorithm boosts more than likes.
- **Hashtags ≤ 3** — anything more reads as spammy in 2025.
