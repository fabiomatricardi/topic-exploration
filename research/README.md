# Demand Discovery Playbook

How to find out what your readers actually need — before you build anything.

Wes Pearce's rule, adapted from *3 Places I'd Look for Digital Product Ideas with a Small Substack*:
> You're looking for **one problem — not ten**. And you can start researching before your comment section gets busy.

This playbook turns that into a repeatable weekly habit. Everything you find goes into [`demand-log.md`](demand-log.md). Ideas that survive scoring become candidates in `../products/next_products.md`.

---

## 1. The principle: you are collecting *problems*, not topics

A topic is "local AI". A problem is *"I downloaded three models, none of them load, and I don't know which one to delete."*

Three things make a problem worth a product:

1. **Repetition.** The same sentence, or close variants, shows up in several unrelated places.
2. **Cost.** People have already tried to solve it (time, money, or quitting). Quitters are the strongest signal — they left the thread, but they still have the problem.
3. **Fit.** You are only a few steps ahead of them on *this specific* problem. You don't need to be the world expert; you need to have already solved it once.

Rule of thumb: **if you can't find the reader's exact words, you haven't found a problem yet — you've found a topic.** Their words become your sales copy later.

---

## 2. Your source list

### Tier 1 — read every week (15 minutes)

| Source | What to look for | How to search |
|---|---|---|
| **r/LocalLLaMA** | "overwhelmed", "which model", "doesn't work", "slow", "OOM", beginner posts with 0 replies | `site:reddit.com/r/LocalLLaMA beginner overwhelmed 2026` |
| **r/LocalLLM, r/ollama, r/llamacpp** | install failures, tool-choice paralysis, "stop using X" debates | `site:reddit.com/r/ollama frustrated install` |
| **r/AIPractitioner, r/vibecoding** | "what should I build", "got stuck", "fix spiral", non-programmers building | `site:reddit.com/r/vibecoding stuck beginner` |
| **r/learnpython, r/learnmachinelearning** | "am I too old", "no CS degree", "where do I start" | `site:reddit.com/r/learnpython over 40` |
| **Your Medium earnings** | which articles earn vs. which get claps — earnings are the honest metric | export or open each article's stats page monthly |
| **Your kit.com + email replies** | questions readers actually hit reply to ask | weekly inbox sweep |

### Tier 2 — read every month (15 minutes)

| Source | What to look for | How to search |
|---|---|---|
| **Amazon 2–3★ reviews** of local-AI / prompt-engineering / Python books | "good but no examples", "I still don't know where to start", "outdated by chapter 4" | search books on llama.cpp, local LLMs, ChatGPT guides; sort by *critical* reviews |
| **Competing Substack/Kit newsletters' comments** (local AI, privacy, older-beginner niches) | the questions their readers ask that *they* don't answer | open the comment threads of their last 5 posts |
| **Hugging Face model pages + GitHub issues** (llama.cpp, OpenCode, LM Studio) | recurring support complaints, unanswered how-do-I questions | search issues for "beginner", "Windows", "documentation" |
| **hn.algolia.com** (Hacker News search) | "I tried X and gave up" stories | `site:news.ycombinator.com local llm disappointing` |
| **YouTube comments** on "run AI locally" tutorials | "worked until…", "my laptop is X, can this work?" | open the 3 most-viewed beginner tutorials, read newest comments |

### Tier 3 — after every product launch (one-off harvest)

- Every reply and question from your 12-day campaign → log it verbatim.
- Every refund request or confused buyer → the confusion point *is* the next product or the next chapter.
- Every "dumb question" (Wes: *the people asking weren't looking for the world's leading expert*) → FAQ material and objection-handling copy.

---

## 3. Query templates that actually work

Copy-paste and swap the bracketed word:

```
site:reddit.com/r/LocalLLaMA [beginner] [overwhelmed OR stuck OR frustrated] 2026
site:reddit.com/r/learnpython "no computer science" AI
site:reddit.com/r/AIPractitioner "still don't know how to code" weekend
"[your topic] I tried" reddit
"[competing product name] review" complaint OR refund OR "waste"
"[book title] review" "but" OR "disappointed"
"what should I build" cursor OR claude code beginner
how to [task] without [cost/requirement your product removes]
```

**Buying-intent queries** (these tell you people will pay, not just read):

```
best course to [outcome] for beginners
"[product name] vs" — comparison searches mean people have a wallet out
"is [product] worth it reddit"
"[price] course" review
```

**Rules for meaningful web search:**
- Always collect **exact sentences**, not summaries. Put quotes in the log.
- Count frequency. "Seen 4× this month in 3 subreddits" beats "someone said this once".
- When you find *one* thread with 200+ comments, read **all** of them — that's a month of research in one sitting.
- Search for what people already **buy** before you search for what they complain about. Complaints + existing purchases = a market. Complaints alone = venting.

---

## 4. The 30-minute weekly ritual

Do it at the same day/time each week. Stop when the timer stops.

| Min | Action |
|---|---|
| 0–5 | Sweep Tier 1 sources with 1–2 queries each. No reading yet — just harvest titles/quotes. |
| 5–15 | Open the 3 most promising threads. Read the **original post + the complaints in comments**, not the solutions. |
| 15–25 | Write 1–5 new entries into `demand-log.md` using the exact reader words. |
| 25–30 | Re-score any open entries with new information. If one problem now scores ≥ 16, promote it to `../products/next_products.md`. |

**Monthly add-on (15 min):** Tier 2 sweep + update your Medium earnings column.

---

## 5. Scoring a logged problem

Score each dimension 1–5 in `demand-log.md`:

- **Frequency** — how many independent places you've seen it (5 = everywhere this month).
- **Pain** — how much time/money/quit-frustration it costs them (5 = "I gave up").
- **Fit** — how close you are to having already solved it (5 = you shipped a product around it).
- **Willingness to pay** — is anyone already buying a solution, at what price? (5 = competitors charge $99+ and get buyers).
- **Reach** — can you reach these people through your existing channels? (5 = they're already your subscribers).

**Score ≥ 16 → candidate product.** Score < 12 → keep logging or discard. The point is to let *evidence* rank your ideas instead of enthusiasm.

---

## 6. Red flags — signals that look like demand but aren't

- **High applause, zero replies.** Your quantum-computing deep-dives can earn claps and no sales. Earnings and replies > applause.
- **Trend topics** ("the next big model dropped"). They spike and die; your product must sell for a year.
- **Problems only experts have.** If solving it requires a GPU farm, your 40s/50s audience can't apply it — and can't buy the follow-up either.
- **"Everyone would like this" problems.** If the fix requires ten steps across ten tools, it's a *product* problem, not a *product*.
- **Your own curiosity only.** Wes's first product flopped because he built what *he* thought readers needed. Log the frequency honestly.

---

## 7. How this connects to the rest of the repo

```
research/README.md      ← this file: the method
research/demand-log.md  ← where findings are collected and scored
research/reader_profile.md ← who the reader is, in their own words
products/next_products.md  ← scored problems turned into product candidates
products/product_C_outline.md ← the one we're building first
campaigns/C_launch_5+7.md ← 5 prep days + 7 selling days, full copy
```

After each campaign, feed the replies back into the log (Tier 3). That's the loop Wes describes: *every product he has was a question his readers asked him repeatedly first.*
