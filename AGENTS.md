# AGENTS.md — Operating Manual for This Project

Read this file first in any new session. It tells you what this repo is, the rules it follows, and exactly how to run the next exploration.

---

## 1. Project context

**Purpose:** help Fabio discover, validate and ship **feasible digital products** built from his existing AI content (Medium publication + Substack), sold through kit.com.

**The person:**
- Fabio — *"The Poor GPU guy"*. 50 years old, philosophy degree, no CS background, self-taught Python/AI. By day: industrial control-process automation engineer.
- Voice: plain English, fellow traveler not salesman, honest about hardware, never mocks beginners.
- Slogans: **"Your AI, Your Rules."** · **"It is never late to start."**

**The audience:** 40s–50s, grew up with DOS, computer-fluent but non-programmers. Privacy-first, 30 min/day or one weekend morning, no GPU. They buy *one clear path*, not information.

**Current focus:** **Product C — "First Real App in 4 Weekends"** ($67 launch → $97). Full outline done, 12-email 5+7 campaign drafted. Lead magnet (*"Which local-AI setup fits YOUR machine?"*) to be built in parallel.

---

## 2. Folder structure

```
.\                           AGENTS.md (this file) · README.md (navigation)
│
├── my_articles\             READ-ONLY source: his Medium articles (titles, tone,
│                            topics, earnings_usd = honest performance metric)
├── my_products\             READ-ONLY source: copy of already-published products
├── wes_strategy\            READ-ONLY source: Wes Pearce's Substack emails/essays —
│                            the product/monetization methodology
│
├── research\                ← ALL new research findings live here
│   ├── README.md            Demand Discovery Playbook (sources, queries, ritual, scoring)
│   ├── demand-log.md        Every logged problem: quotes + scores. Open vs Closed.
│   └── reader_profile.md    Who the reader is, in their own words + objections
│
├── products\                ← Product candidates and outlines
│   ├── next_products.md     4 candidates (A/B/C/D) + lead magnet + decision matrix
│   └── product_C_outline.md Full outline of the product being built first
│
├── campaigns\               ← Launch campaigns
│   └── C_launch_5+7.md      12 full emails (5 prep + 7 selling) + Wes-rule appendix
│
└── outputs\                 Generated assets (exports, images, scripts) when needed
```

**Rule:** `my_articles\`, `my_products\`, `wes_strategy\` are **source material — never edit, move or delete them.** All new work goes into `research\`, `products\`, `campaigns\` (and `outputs\` for generated files).

---

## 3. Hard rules

1. **Evidence over enthusiasm.** No product gets an outline unless it exists as a `demand-log.md` entry with **score ≥ 16** (F+P+Fi+W+R, each 1–5 — see `research/README.md` §5).
2. **Reader's exact words.** Log quotes verbatim with source URL. Their sentences become sales copy; summaries are worthless.
3. **One problem, not ten.** Every product solves a single problem (Wes rule). If you can't state it in one sentence, it isn't a product.
4. **No fabricated proof.** Testimonials only from real buyers/beta readers. Until a real quote exists, keep the `[PLACEHOLDER — …]` slot in campaign files.
5. **One P.S., one product** in every email — never a list of links (a list reads like a catalog).
6. **Voice:** Fabio's tone as in `my_products\` files ("Ciaooooo, Fabio here…"). Plain English, jargon explained immediately, honest hardware limits, no hype.
7. **Local / free-to-run / privacy** is the brand: every product must be usable at $0/month on a modest machine, or explicitly say who it isn't for.
8. **Write in English** (repo language). Keep files in Markdown, one file per concern, cross-link with relative paths.
9. **Never announce, always refer.** Product promotion happens through contextual P.S. links and story-about-the-problem content (Wes rule, §7 below) — cold "buy my stuff" emails are the failure mode.

---

## 4. The exploration loop (how this repo works)

```
① RESEARCH (30 min/week)
      ↓  queries + sources in research/README.md §2–3
② LOG
      ↓  append entry with exact quotes → research/demand-log.md
③ SCORE  (F+P+Fi+W+R, each 1–5)
      ↓  ≥16 → promote ; <12 → discard
④ CANDIDATE
      ↓  one-page entry in products/next_products.md
⑤ OUTLINE (only for the one chosen product — one at a time)
      ↓  products/<product>_outline.md
⑥ CAMPAIGN (5 prep + 7 selling, full copy)
      ↓  campaigns/<launch>.md
⑦ LAUNCH → harvest replies/refunds (Tier 3) → back to ①
```

---

## 5. Steps for a new run (session checklist)

1. **Read this file**, then `research/demand-log.md` → *Open entries* and `products/next_products.md` → *decision matrix* (this is the repo's memory: what's explored, what's next).
2. Run the **weekly 30-min ritual** from `research/README.md` §4 (Tier 1 sources, queries in §3).
3. **Append new log entries** to `research/demand-log.md` using the template: exact quote + source + 5 scores + notes. Re-score existing entries if new evidence arrived.
4. If an entry scores **≥ 16**: add or update its one-page candidate in `products/next_products.md`.
5. **Check the build order** (§6) before writing any outline — don't build out of order just because an idea is exciting.
6. Write/refresh the **outline** (`products/<X>_outline.md`), then the **campaign** (`campaigns/<X>_launch_5+7.md`, structure: 5 prep days + 7 selling days + Wes appendix).
7. **Update status lines** in `next_products.md` and the campaign header so the next session knows where things stand.

---

## 6. Where to find explored ideas & how to move to the next one

| Question | Where the answer lives |
|---|---|
| What ideas have already been explored? | `research/demand-log.md` — **Open entries** (7 seeded, scores 17–23) vs **Closed/discarded** table |
| Which products are candidates and how do they rank? | `products/next_products.md` → *Decision matrix* |
| What is being built right now? | `products/product_C_outline.md` header (**Status** line) |
| What's ready to send? | `campaigns/C_launch_5+7.md` (12 emails, full copy) |
| What do I research next? | Lowest-scored open entries + empty *Closed* table = keep hunting for ≥16 problems |

**Build order (agreed):**

```
IN FLIGHT:  C — First Real App in 4 Weekends   (outline + campaign done → execute)
PARALLEL:   Lead magnet "Which local-AI setup fits YOUR machine?" (free/€9, feeds all)
NEXT:       A — When It Breaks (troubleshooter, $19–29)  ← completes the No Probl package
THEN:       B — Your Docs, Your Brain (local RAG, $37–49)
LAST:       D — Restore Your Old Photos ($19) → VALIDATE FIRST (€9 preorder, ≥10 sales/72h
            before writing any outline — its log score is 17, the weakest)
```

**Gates & stop rules:**
- Move to the next product only after reviewing the current launch's 30-day metrics (campaign appendix §4): Day-7 sales < 15 or refunds > 5% → **fix before building anything new** (usually a Weekend-0 onboarding fix, not a pitch fix).
- A new candidate displaces the queue only by **beating the decision matrix** (demand score + asset reuse + price headroom − effort).
- If two problems log ≥ 16, they don't merge — pick the one with the better *Willingness-to-pay* score.

---

## 7. APPENDIX — The Wes rule: evergreen mentions after Day 7

Wes Pearce's pattern (observed across his emails): **he always introduces new content, but every email quietly references an existing product — never a cold announcement.** After a campaign ends, this is how the store keeps selling without launches. *(Source: `campaigns/C_launch_5+7.md` §Appendix — keep both copies in sync.)*

### 7.1 The permanent P.S. rotation
Every email ever sent ends with **one** P.S. linking **one** product, rotated by context:

| If today's content is about… | P.S. links to |
|---|---|
| Getting started / free AI / first steps | Zero to AI (€17) |
| Agents, OpenCode, "build something" | Weekend AI Agent Toolkit ($7.99) |
| Python, learning by building | Ctrl+Think (€27) |
| llama.cpp, models, quantization, speed | No Probl-LLAMA.cpp (€7.90) |
| Building a full app, going further | First Real App in 4 Weekends ($97) |
| Troubleshooting, errors | A: When It Breaks *(when it exists)* |

Rule: **one product, one link, one sentence** — never a list of five. A list reads like a catalog; a single line reads like a friend remembering something useful.

### 7.2 Placement checklist (set once, sells forever)
- [ ] **Welcome email:** story + one door (the $7.99 Toolkit or free checklist)
- [ ] **About page:** your arc + the ladder (free → €17 → $67/97), with the napkin-test sentence
- [ ] **Every Medium article PS:** the Weekend Toolkit banner; add a second, text-only line for Product C in "build-your-own-app" articles
- [ ] **Substack Notes:** one evergreen note per week quoting a *reader problem* → soft link
- [ ] **Auto-sequence for non-buyers in kit.com:** Day 3 after cart close → "still thinking? here's the $7.99 door"

### 7.3 The content → product map (never announce, always *refer*)
Write about the **problem** (story about the problem, not the finished solution) and let the P.S. be the deep end:

| Upcoming content idea | Product it feeds |
|---|---|
| "Why your AI app keeps eating your RAM" (Control Room rule 1) | Product C |
| "5 things I fixed in my first app" | Product C |
| "The error I see most on Reddit, explained" | A: When It Breaks |
| "Ask your own PDFs a question" | B: Your Docs, Your Brain |
| "Which local AI fits your laptop?" | Free checklist (lead magnet) |

### 7.4 Metrics to review 30 days after close
Sales by source (kit link vs Medium vs Substack) · open rates per day (Day 2 proof and Day 5 math should be the highest) · reply themes → feed into `research/demand-log.md` (Tier 3 harvest) · refund reasons → Weekend 0 onboarding fix.

---

*When in doubt: research before building, one product at a time, the reader's words over your assumptions.*
