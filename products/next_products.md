# Next Products — 4 Candidates

All four are scored from `../research/demand-log.md` (log IDs in brackets). One of them — **C** — has a full outline in [`product_C_outline.md`](product_C_outline.md) and a launch campaign in `../campaigns/C_launch_5+7.md`.

**Shared positioning:** every product answers the same slogan — *"Your AI, Your Rules."* Everything is **local, free-to-run, honest about hardware**, and written for people whose best coding year was `PRINT "HELLO"`.

---

## The ladder (where each product sits)

```
FREE / €9  ──► Lead magnet: "Which local-AI setup fits YOUR machine?"
                    │ (feeds all three below)
$7.99–€37  ──► [existing] Weekend AI Agent Toolkit · No Probl-LLAMA.cpp
                    │              Ctrl+Think · Zero to AI · FLUX prompts
$19–€29    ──► A: When It Breaks (troubleshooter)
$37–€49    ──► B: Your Docs, Your Brain (private local RAG)
$67–€97    ──► C: First Real App in 4 Weekends   ◄── BUILDING FIRST
$19        ──► D: Restore Your Old Photos (consumer hook)
```

---

## Lead magnet (free or €9) — "Which Local-AI Setup Fits YOUR Machine?"

- **Problem [D-001]:** *"The sheer number of tools is overwhelming."*
- **Format:** 6-question interactive checklist → one-page personalized verdict (Ollama vs LM Studio vs llama.cpp, which model class for your RAM, one download link). Delivered as a PDF or a tiny local script.
- **Job:** email capture on Substack/kit, and the top of every funnel. One page to build. Mention it in *every* campaign as the free first step.

---

## A — "When It Breaks: The Local AI Troubleshooter" · $19–$29

- **Problem [D-002]:** *"It breaks and I'm alone with the error."*
- **Demand sources:** r/LocalLLaMA threads (`llama.cpp is slow`, `OOM`, `GPU not detected`, `garbled output`), InsiderLLM's symptom→fix guide (exists *because* this demand is huge), GitHub issues.
- **Format:** **symptom → fix decision tree** (PDF) + a diagnostic `.bat` that collects your system facts (RAM, GPU, driver, model file) and prints the matching fix page. 20–30 most common symptoms.
- **Your unfair advantage:** you already ship the installer (No Probl-LLAMA.cpp), the benchmarker and the quantization series — this product *completes* that package and raises its price.
- **Effort:** medium — mostly writing + one small script. Evergreen; update quarterly (an "updated for llama.cpp 2026-XX" line is sales copy in itself).
- **Cross-sell:** the #1 upgrade path from every existing €7.90–€17 buyer.

---

## B — "Your Docs, Your Brain: Private Local RAG in a Weekend" · $37–$49

- **Problem [D-005]:** *"Chat with my own documents — without sending them anywhere."*
- **Demand sources:** **your own best-earning Medium article ($151, keyword search/RAG)**; DIY guides for Open WebUI+Ollama / PrivateGPT all carry "setup is fiddly" complaints; professionals with NDAs (your OpenCode privacy audience).
- **Format:** step-by-step guide + **one-click installer** (you've built one before) + prompt pack ("summarize this contract", "what did we decide about X"). Stack: local embeddings + your existing llama.cpp base.
- **Why it sells:** the outcome is emotional and concrete — *"ask your own filing cabinet questions"*. Strong for 40s/50s professionals with a decade of PDFs.
- **Effort:** high (installer + chunk of testing) — do after C.
- **Cross-sell:** natural step *up* from Zero to AI; the free lead magnet feeds it.

---

## C — "First Real App in 4 Weekends" · $67–$97  ◄ RECOMMENDED FIRST

- **Problems [D-003 + D-004 + D-006]:** *"I don't know what to build"*, *"the fix spiral"*, *"am I too old for this."*
- **Demand sources:** your two OpenCode articles (**$133 + $68 — your top-2 2026 earners**); r/AIPractitioner *"I built a real app in four weekends. I still don't know how to code"*; comparable cloud courses sell **$49–$249** (AnyoneBuilds $99, CreateYourAppWithAI $100–200, DeepLearn $249, buildDay workshop) — **and none of them serve the local-first, zero-cost, 40s/50s buyer.**
- **Your wedge:** every competitor assumes Cursor Pro ($20/mo), Claude Code, Vercel, Supabase. You deliver the same outcome with **OpenCode + free local models + $0/month**, wrapped in your Control-Room reliability rules (kill switch, batch launchers, reproducibility) — the documented cure for the fix spiral.
- **Format:** 4 weekend projects, one per weekend: plan → build → harden → ship, each ending in something that runs on *their* machine. Full outline: [`product_C_outline.md`](product_C_outline.md). Campaign: `../campaigns/C_launch_5+7.md`.
- **Effort:** highest of the four — but it's mostly re-assembly of content you've already published (OpenCode series + Weekend Toolkit + Control-Room rules).

---

## D — "Restore Your Old Photos This Weekend" · $19

- **Problem [D-007]:** nostalgic, mainstream, zero-code.
- **Demand sources:** your existing article (*blinking cursor… blurry photo*, $6 on Medium — read as *interest without a product*, not as demand proof); the wider "restore old photos" market is enormous and paid (MyHeritage, Remini).
- **Format:** guide + 3 scripts (upscale, denoise, face-enhance) + a double-click launcher. Local, free, private — *your photos never leave the PC* is a strong ethical hook older buyers get instantly.
- **Why it's #4:** Medium $6 suggests readership rather than buyer intent — **validate first**: publish a Substack post + one kit.com email with a €9 preorder link; if ≥10 sales in 72h, build it.
- **Effort:** low. Great candidate for a December gift-season slot.

---

## Decision matrix (scored)

| | Demand score (log) | Reuses existing assets | Price headroom | Build effort | Verdict |
|---|---|---|---|---|---|
| **C** | 23 + 23 + 20 | ★★★★★ (OpenCode series, Toolkit, Control Room) | ★★★ ($67–97) | High | **Build first** |
| **A** | 23 | ★★★★★ (installer + quantization) | ★★ ($19–29) | Medium | Build second — completes No Probl package |
| **B** | 20 | ★★★★ ($151 article, installer skill) | ★★★ ($37–49) | High | Build third |
| **D** | 17 | ★★★ (existing article) | ★ ($19) | Low | Validate cheaply, then maybe |

**Next action:** execute `../campaigns/C_launch_5+7.md` for product C; start the lead magnet as a parallel one-week side task.
