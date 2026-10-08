---
post_id: "895a4cd88b59"
title: "The right way to use Opencode is to build your own app"
subtitle: "A showcase and guide to build 3 projects with Opencode and why you should start doing it right now."
published: "2026-07-03T09:36:00.849Z"
url: "https://medium.com/@fabio.matricardi/the-right-way-to-use-opencode-is-to-build-your-own-app-895a4cd88b59"
earnings_usd: 68
---

# The right way to use Opencode is to build your own app

*A showcase and guide to build 3 projects with Opencode and why you should start doing it right now.*

---

![A technical infographic from “CHAOS ENGINE,” representing chaotic AI execution to “DOWNSTREAM AUTOMATION.”. “OPENCODE” is the tool to build clarity](../assets/1_rTC5MhNqEdichLQJgWb2gg.png)

*The Blueprint: Routing unstructured AI reasoning into 100% reliable Python pipelines*

AI agent harnesses are undeniably the defining trend of the first half of 2026. Everywhere you look, developers and tech enthusiasts are building with or talking about tools like Claude Code, OpenCode, Pi.dev, and the rest of the emerging local autonomous landscape.

The promise is intoxicating: a generous stream of open-source capabilities running locally on your hardware, handling complex tasks without draining your wallet on external API tokens. It feels incredibly powerful.

But it is also incredibly dangerous.

If we surrender full autonomy to these multi-step agent loops without guardrails, we risk sliding into a new kind of technical debt — a form of “AI slavery” where we become subservient to tools we can neither predict nor truly control.

[**Harness Agents can become the next AI slavery… unless you do this.**  
*How to use your Agents to create a pipeline that feeds downstream automation and expect the same results to come out of…*medium.com](https://medium.com/artificial-intel-ligence-playground/harness-agents-can-become-the-next-ai-slavery-unless-you-do-this-82895c1055a2 "https://medium.com/artificial-intel-ligence-playground/harness-agents-can-become-the-next-ai-slavery-unless-you-do-this-82895c1055a2")

By the way I will show you in this article 5 projects you can build with Opencode in few hours:

```
- a LLM gateway that routes your traffic through your API, with a fallback  
- a Telegram bot scheduler, that reads every hour new messages in your   
  bot channel, extract text from the links and send by email a Digest   
  about them  
- a Karpathy syle LLM-wiki on your personal knowledge base, with   
  built in knowledge graph that you can query: all with python pipelines,   
  no agents
```

---

![](../assets/1_HptVmPxYefOgWgJXvG4UrA.png)

### The Chaos Engine: The Challenge of Unpredictable Agents

The core problem with running raw, unconstrained agent harnesses in a real-world workflow is simple: **nondeterminism and unvalidated compute.**

When you launch an agent to solve an open-ended task, you have no baseline guarantee of what will happen next. You don’t know if it will solve your problem in three tool calls or spin out into a hundred loops, chewing up your local CPU or iGPU bandwidth on redundant inference.

Worse yet, agent harnesses behave differently every single time.

Even if you clone the exact same repository, use the exact same model weights, and set up the identical environment across two different computers, you have no promise of reproducibility. A slight variance in response formatting or a minor shift in context window handling can send the agent down an entirely different logical path.

For critical everyday tasks, this behavior is a non-starter.

> If a system cannot guarantee that Input A will reliably yield Output B every single time, it isn’t an engineering tool… it’s a slot machine.

So, how do we fix it without losing the magic of local intelligence?

---

PS: I created a startup toolkit so that you can get started and ready to go in just a weekend.

[![](../assets/1_pCveiqWQabJjqaet_1SHEw.png)](https://build-your-own-ai.kit.com/weekend-ai-agent-toolkit)

*Click to learn more*

---

![](../assets/1_76SykBjceRQPz1BU7eJPCQ.png)

### The Blueprint: Shifting from Autonomous Chaos to Downstream Automation

If you want your local AI setup to be genuinely useful in your everyday workflow, you have to change your architectural philosophy.

Instead of letting an agent run wild as an isolated, black-box decision-maker, you must treat OpenCode as an **intelligent generation engine that feeds reliable, deterministic downstream automation pipelines.**

The goal isn’t to build an all-knowing oracle that might hallucinate or loop forever.

The goal is to build tight, targeted Python utilities where OpenCode handles the messy, unstructured language translation, while your hardcoded downstream code handles the exact execution, file writing, and routing.

> When you bind the LLM inside a predictable pipeline, you get the reasoning power of AI combined with the 100% reliability of classic software engineering.

To prove exactly how this works in practice, we are going to go through three specific apps you can build right now to reclaim control over your local workspace. Here is a quick look at what we are building:

![](../assets/1_-bto--FssBH3LNpJ0WIKVw.png)

> **The rule of thumb:** We are not building these apps to let an agent think for us. We are building them so OpenCode can handle the data translation, letting our Python automation do the heavy lifting reliably, every single time.

---

![](../assets/1_1TCMOaOvDLNvic8VahU5nQ.gif)

### Project 1: The Multi-LLM Gateway

What if you are free from dealing all the time with API settings, BASE\_URL and models? What if you set your own Gateway and send all the traffic to it (maybe running on an ald pc or miniPC in your network?)

[**GitHub - fabiomatricardi/multiLLMgateway: Ollama and OpenAI compatible Gateway routing trattic to…**  
*Ollama and OpenAI compatible Gateway routing trattic to free LLM provider - fabiomatricardi/multiLLMgateway*github.com](https://github.com/fabiomatricardi/multiLLMgateway "https://github.com/fabiomatricardi/multiLLMgateway")

The foundation of a smooth local AI workspace is cross-compatibility. If you have automation scripts or desktop tools built to expect a standard local endpoint, changing them to point to various cloud providers usually requires editing code across multiple files. This app completely removes that friction.

#### The Problem This App Solves

Most modern AI development tools and extensions are configured to talk to a standard OpenAI-compatible API endpoint layout. However, switching between different cloud APIs requires managing different SDK structures, base URLs, and authentication methods.

The **Multi-LLM Gateway** solves this by acting as a universal local proxy server. It listens locally on port `11434` (hijacking Ollama's default port purely for local convenience) but it exposes the widely adopted **OpenAI API standard endpoints** (`/v1/chat/completions`).   
When your local applications send an OpenAI-formatted payload to this port, the gateway intercepts it, checks your user-configured API keys and model parameters, and routes the call to the appropriate cloud provider.

#### How to Build It with OpenCode

You are using OpenCode here to construct a proxy server that unifies multiple external cloud APIs under a single local standard.

1. **Implement the OpenAI Route Contract:** Instruct OpenCode to spin up a local Python server (such as FastAPI) that explicitly listens on port `11434` and handles the standard OpenAI route layout, primarily the `POST /v1/chat/completions` endpoint.
2. **Build the Key and Cloud Routing Layer:** Create a configuration setup where the user defines their cloud API keys and target model names. OpenCode can generate the routing logic that parses the incoming model payload string and translates it to the respective cloud provider’s official SDK client call.
3. **Prompting Strategy:** Ask OpenCode:

> *“Write a Python FastAPI application that runs locally on port 11434. It must expose a standard OpenAI-compatible route at* `/v1/chat/completions`*. Inside the handler, parse the payload, check the specified model string, and use the correct Anthropic, Google, or OpenAI API client to process the request, returning the response in the exact OpenAI format."*

#### Engineering Hints with OpenCode

- **The Universal Payload Translation:** While the gateway accepts an OpenAI-standard payload on the front end, it needs to translate that into the correct structure for the destination cloud if you are routing to a non-OpenAI provider like Anthropic. Remind OpenCode to safely map parameters like `max_tokens`, `temperature`, and especially the conversion of a system message into the provider-specific field structure.
- **Stream Chunk Standardization:** If your downstream applications expect streaming tokens (`stream=true`), your proxy must capture the streaming chunks from the cloud provider, translate them on the fly, and yield them back to the client in the standard OpenAI `data: {...}` Server-Sent Events (SSE) format. Instruct OpenCode specifically to handle the asynchronous generator loop cleanly to avoid dropping connections mid-sentence.

---

![](../assets/1_sZsajpJP-GgaqKG2lv0mXw.gif)

### Project 2: The Karpathy-Style Knowledge Base & Wiki Database

Not relying on Agent Harness and still getting a cool knowledge base app? This is for you!

[**GitHub - fabiomatricardi/KB-Database: a standalone knowledge base db with BM25 and chat and Ollama…**  
*a standalone knowledge base db with BM25 and chat and Ollama LLM - fabiomatricardi/KB-Database*github.com](https://github.com/fabiomatricardi/KB-Database "https://github.com/fabiomatricardi/KB-Database")

This project brings the “Second Brain” philosophy to life by turning a simple folder of static text files into an interconnected network of data you can easily query.

#### The Problem This App Solves

Most people manage their personal knowledge base using a chaotic folder of loose Markdown files. Over time, as notes pile up, it becomes nearly impossible to track how different topics relate to one another without manually linking them.   
Relying on an unconstrained AI agent to read all your notes on the fly is slow, expensive, and highly prone to hallucination.

[**I Built an AI Second Brain to cure my information overload. And here is how.**  
*How an oil and gas engineer used the free Opencode coding agent to automate note-taking, kill the folder chaos, and…*medium.com](https://medium.com/artificial-intel-ligence-playground/i-built-an-ai-second-brain-to-cure-my-information-overload-and-here-is-how-5d48ed2bfe62 "https://medium.com/artificial-intel-ligence-playground/i-built-an-ai-second-brain-to-cure-my-information-overload-and-here-is-how-5d48ed2bfe62")

The **KB-Database** solves this by establishing a strict, structured pipeline built with a modern **Python (FastAPI) and Vue.js** architecture, cleanly packaged so it can compile into a single executable file.   
Instead of forcing an AI to blindly scan raw files every time you ask a question, this app splits your workflow into two explicit, deterministic steps: one section dedicated solely to file ingestion and indexing, and another dedicated to building and querying the knowledge graph.

To ensure this app can run or compile on literally any target Windows machine (**even if Python isn’t installed** ) the project uses a modern developer stack powered by `uv` instead of traditional `pip`. The repository includes pre-built `.bat` scripts that handle the entire environment lifecycle: one to launch the app instantly in place, and another to bundle the entire project into a completely standalone `.exe` file.

> ⚠️ **Important Privacy Guardrail:** Because this application leverages free public API endpoints — specifically the free tiers for Google Gemini and NVIDIA models configured via the app’s settings tab — **this setup is not intended for handling NDA-protected, corporate, or PII (Personally Identifiable Information) data.** It is designed for personal knowledge synthesis and public-facing research.

#### How to Build It with OpenCode

You can use OpenCode to generate the frontend-backend communication layout, the environment configurations, and the automation scripts that make deployment effortless.

1. **Scaffold the App Layout:** Instruct OpenCode to generate a FastAPI backend that serves a unified Vue.js single-page application. Ensure it builds the configuration tab where you can input your Gemini and NVIDIA free API keys and select your preferred models.
2. **Write the Environment and Automation Scripts:** Have OpenCode help you write the `.bat` orchestration files that invoke `uv` to pull down a self-contained Python runtime, install dependencies into an isolated virtual environment, and trigger the compilation build.
3. **Prompting Strategy:** Ask OpenCode:

> “Write a Windows batch file (`.bat`) that checks for the presence of the `uv` package manager. If available, use `uv run` to spin up a transient, self-contained Python environment to execute our FastAPI/Vue script without modifying the host system's global environment variables. Also, provide a second batch script that calls PyInstaller via `uv` to compile the entire project into a single executable binary."

#### Engineering Hints with OpenCode

- **The Single-Executable Challenge:** Because this app is designed to be bundled into a single standalone executable, OpenCode needs to handle file paths carefully. Remind OpenCode to use relative asset pathing (`sys._MEIPASS` checks in Python) so that the Vue.js frontend static assets render correctly once compiled into a single binary.
- **API Rate-Limit Handling:** Free-tier endpoints for Gemini and NVIDIA often carry strict requests-per-minute (RPM) limits. When prompting OpenCode to build the ingestion loop, explicitly instruct it to write an asynchronous batch-processing mechanism with built-in sleep throttles (`asyncio.sleep`) to prevent the ingestion pipeline from crashing due to rate limits during a heavy folder import.

---

![](../assets/1_k_NMBx1eQMP69t0shWEdVw.gif)

### Project 3: The Telegram Digest Scheduler

When you browse news on your phone and you don’t have an easy way to bookmark them or take notes… why don’t we send all the links to a Telegram chatbot and this app handles a Digest for you?

[**GitHub - fabiomatricardi/TelegramScheduler: flask GUI app scheduler to check your Telegram Bot and…**  
*flask GUI app scheduler to check your Telegram Bot and send a Digest to your email form the posts …*github.com](https://github.com/fabiomatricardi/TelegramScheduler "https://github.com/fabiomatricardi/TelegramScheduler")

This project tackles the information firehose by transforming a noisy chat stream into a clean, structured, and regular reading list delivered straight to your inbox.

#### The Problem This App Solves

We all stumble across fascinating articles, PDFs, or deep-dive threads while browsing on our phones during the day. The problem is capturing them. Bookmarking apps become digital graveyards, and leaving fifty browser tabs open drains your phone’s battery and your focus. Trying to run a complex, real-time agent system just to track your reading list is massive overkill that burns unnecessary compute.

The **Telegram Digest Scheduler** solves this by leveraging an app you already open a hundred times a day: **Telegram**. Instead of overcomplicating things, the workflow is brilliantly simple.   
Whenever you find an interesting document, article, or post on your phone, you just **forward it directly to your personal Telegram bot**.

Behind the scenes on your local machine, a Python script wakes up on a schedule (like every hour), quietly collects everything you’ve forwarded from your phone, scrapes the full text from the links, summarizes the material, and emails you a beautiful, unified digest.

![](../assets/1_LOw0Z9TtvEjgivxKRY5GTQ.png)

*this is the email I receive…*

#### How to Build It with OpenCode

You can use OpenCode to integrate Telegram bot polling, text extraction tools, and local LLM endpoints into a single automated chain.

1. **Build the Telegram Bot Ingestion Layer:** Instruct OpenCode to use `telepython` or standard HTTP polling to read incoming messages sent to your specific bot token, extracting the raw text or shared URLs.
2. **Implement Content Extraction:** Have OpenCode build a deterministic scraper layer using `trafilatura` or `BeautifulSoup` to visit the forwarded links, strip out the website clutter (ads, sidebars), and isolate the actual text you want to read.
3. **Prompting Strategy:** Ask OpenCode:

> “Write a Python script that polls a Telegram bot using my secret bot token. Fetch all unread messages forwarded by the user. If a message contains a URL, extract the main article text, bundle all extracted texts together, and use an OpenAI-compatible completion endpoint to generate a structured email digest.”

#### Engineering Hints with OpenCode

- **The HTML Scraping Trap:** OpenCode will often default to a generic `requests.get()` scraper that breaks completely when hitting modern web pages protected by cookie banners or heavily dependent on JavaScript rendering. Instruct OpenCode to implement robust exception handling during the link extraction phase, using a fallback tool like `trafilatura` or cleanly bypassing scraping failures so a single bad URL doesn't hang your entire scheduled routine.
- **Environment Configuration & API Layering:** This project relies on the popular `opencode-to-openai` gateway, which maps OpenCode's underlying command-line engine and its free inference models into a standard OpenAI-compatible API endpoint layout. When prompting OpenCode, instruct it to pull all parameters from a local `.env` file. This file must contain your local gateway endpoint details, the secret `TOKEN` for your Telegram bot, and a dedicated **Gmail App Password** generated specifically for this script to handle the automated email dispatch securely without exposing your master account credentials.

---

![](../assets/1_SgBL7UtcwFGRmj_ttvTyUw.png)![](../assets/1_TkkPPLCeMx6O61n5LZQkfw.png)![](../assets/1_oO6Ml0-QeTIs7HICkr7vEg.png)

### Stop Playing the Slots, Start Engineering

The tech world in 2026 is obsessed with letting AI agents run wild, treating them like digital magic mirrors that can magically solve open-ended problems. But as we’ve seen, running unconstrained agent loops is an easy way to burn local compute, create unrepeatable workflows, and introduce endless frustration into your daily routine.

> The true power of local tools like OpenCode is found in using them as **highly specialized translation engines** that sit safely inside your own, hardcoded software pipelines.

Build your own lightweight apps!

Whether it’s a proxy gateway that unifies cloud APIs on port `11434`, a standalone knowledge graph powered by `uv`, or a seamless Telegram-to-email digest, you can change the rules of the game. You take the messy, unstructured reasoning of an LLM and channel it into a 100% reliable downstream automation pipeline.

You don’t need a a team of engineers to build your efficient workspace. You just need a free model, a clean Python script, a couple of hours, and the right architectural mindset.

Stop treating local AI like a slot machine.

Open up your terminal, fire up OpenCode, and start building software that works exactly the way you expect it to… every single time.

> want few more ideas?

- 🪪 a HTML link card creator
- 📳 a tweet generator starting from an article or text
- 🧑‍🏫 your personal most used command-wiki, available right away (from the terminal or in a web app suite)
- 👨‍🔧 send documents in your Telegram bot and put them in Markdown to the your local wiki folder for further ingestion

---

I hope you enjoyed the article. If this story provided value and you wish to show a little support, you could:

1. Clap a lot of times for this story
2. Highlight the parts more relevant to be remembered (it will be easier for you to find them later and for me to write better articles)
3. [Write with me on this Publication](https://medium.com/artificial-intel-ligence-playground/subpage/8e83fae83815): there is no better way to learn than writing about it!
4. Follow my publication <https://medium.com/artificial-intel-ligence-playground>

If you want to read more, here are some ideas:

[**The OpenCode revolution: more than just another chatbot**  
*AI Agency under your control and data that never leaves your PC. You don’t need anymore Codex or Claude Code. Part 1 of…*medium.com](https://medium.com/artificial-intel-ligence-playground/the-opencode-revolution-more-than-just-another-chatbot-21706215701f "https://medium.com/artificial-intel-ligence-playground/the-opencode-revolution-more-than-just-another-chatbot-21706215701f")

[**The Agent’s Operating System: why Harness Engineering is your next step to a reliable AI**  
*Think of the model as the CPU and the harness as the Operating System. And here I show you how to do it on your PC.*medium.com](https://medium.com/artificial-intel-ligence-playground/the-agents-operating-system-why-harness-engineering-is-your-next-step-to-a-reliable-ai-211a89d887e7 "https://medium.com/artificial-intel-ligence-playground/the-agents-operating-system-why-harness-engineering-is-your-next-step-to-a-reliable-ai-211a89d887e7")

[**I Built an AI Second Brain to cure my information overload. And here is how.**  
*How an oil and gas engineer used the free Opencode coding agent to automate note-taking, kill the folder chaos, and…*medium.com](https://medium.com/artificial-intel-ligence-playground/i-built-an-ai-second-brain-to-cure-my-information-overload-and-here-is-how-5d48ed2bfe62 "https://medium.com/artificial-intel-ligence-playground/i-built-an-ai-second-brain-to-cure-my-information-overload-and-here-is-how-5d48ed2bfe62")

[**The future of generative AI is vectorless**  
*And why this is not what you think: it is a tragedy!*medium.com](https://medium.com/artificial-intel-ligence-playground/the-future-of-generative-ai-is-vectorless-09ca1ab57bc0 "https://medium.com/artificial-intel-ligence-playground/the-future-of-generative-ai-is-vectorless-09ca1ab57bc0")