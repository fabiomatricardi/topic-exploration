---
post_id: "72483c933787"
title: "The Control Room guide to AI Agents: 6 Rules for shipping reliable apps"
subtitle: "Do like an Industrial Automation Engineer that applies heavy-industry discipline to build, test, and deploy bulletproof local AI…"
published: "2026-07-22T12:21:01.479Z"
url: "https://medium.com/@fabio.matricardi/the-control-room-guide-to-ai-agents-6-rules-for-shipping-reliable-apps-72483c933787"
earnings_usd: 8
---

# The Control Room guide to AI Agents: 6 Rules for shipping reliable apps

*Do like an Industrial Automation Engineer that applies heavy-industry discipline to build, test, and deploy bulletproof local AI…*

---

![](../assets/1_ICw7YXet4O4zAFe1TmlJGQ.png)

Over the past two months, my evenings have looked completely different from my days. [By day, I am a Control Process Automation engineer](https://fabiomatricardi.dpdns.org/) in the oil and gas sector. I design, test, and commission massive automation systems where software loops monitor high-pressure lines and critical valves.

In my world, we don’t deploy code just because it looks pretty; we deploy it because it is safe, predictable, and has failed a thousand simulated stress tests before touching a single physical asset.

By night, however, I’ve been diving deep into a completely different kind of automation: autonomous AI agents.

[**Timer on Delay**  
*When counting to 10 is really a good idea…*medium.com](https://medium.com/predict/timer-on-delay-4aa5d33a88de "https://medium.com/predict/timer-on-delay-4aa5d33a88de")

Using harnesses like `opencode` and local language models running right on my workstation, I discovered a profound shift. I am not a professional software developer. I don't spend years mastering complex syntax or compiler quirks. Yet, using these AI agents, I’ve managed to spin up fully functional, intricate Python applications in mere minutes.

It feels like a superpower. You describe a problem, the agent writes the script, sets up the loop, and hands you an application.

[**The right way to use Opencode is to build your own app**  
*A showcase and guide to build 3 projects with Opencode and why you should start doing it right now.*medium.com](https://medium.com/artificial-intel-ligence-playground/the-right-way-to-use-opencode-is-to-build-your-own-app-895a4cd88b59 "https://medium.com/artificial-intel-ligence-playground/the-right-way-to-use-opencode-is-to-build-your-own-app-895a4cd88b59")

But very quickly, my professional instincts kicked in. I noticed a massive, dangerous gulf between an AI-generated “working demo” running inside a chat box and a truly robust, shippable application that you can hand to a friend, share with a colleague, or run six months from now without a total system crash.

Left to their own devices, AI agents write messy environments, forget how they structured their own code five minutes ago, leave hidden background processes running that eat up your RAM, and create apps that work exclusively on the machine where they were born.

> In industrial automation, we have a saying: *If you haven’t engineered the shutdown, the safety limits, and the deployment footprint, you haven’t engineered anything at all.*

I realized we desperately need a framework for this new era. I took the exact principles we use to commission heavy-industry control rooms: clear specifications, explicit shutdown loops, environmental isolation, and rigorous stress testing . So I spent two months testing them through trial, error, and dozens of broken Python scripts.

Whether you are in your 40s or 50s, a hobbyist, an enthusiast learner, or someone who simply wants to build tools that actually work, this playbook is for you.

Here are the 6 industrial-grade rules to build and ship consistent, high-quality apps with AI agents.

![](../assets/1_JDSt3bkLQMxEom93252ldQ.png)![](../assets/1_P2GaTfIQxzx7yN23KMfA2Q.png)

*always put a clean shutdown button*

### Rule 1: Build the “Kill Switch” Before the Engine (Shutdown & Process Management)

When we design a process plant, the very first thing we map out isn’t how to start the pumps: it’s how to stop them safely in an emergency. In software, especially AI-generated software, we tend to do the exact opposite. We focus entirely on making the app *go*, completely ignoring how it *stops*.

AI agents love creating background tasks. If your app utilizes asynchronous loops, multi-threaded tasks, or local web servers to show a user interface, clicking the “X” in the corner of the window often only closes the visual shell. The engine underneath keeps chugging along silently in your computer’s memory, hogging your CPU and RAM.

Every single application you build with an AI agent must include an explicit, hardcoded cleanup mechanism that terminates its own processes cleanly from within the interface.

Before you let the agent write the core logic, force it to implement a shutdown route in your backend service. Tell your agent:

> “Write an explicit, non-negotiable `/api/shutdown` endpoint that triggers a background thread to safely exit the application process, allowing it to return a confirmation before dying."

Here is the exact FastAPI implementation pattern I force my agents to embed in the `backend/main.py` entry point:

```
import os  
import sys  
from fastapi import FastAPI  
  
app = FastAPI(title="ReliableAgentApp", version="1.0.0")  
# Shutdown endpoint (always present in my playbook)  
@app.post("/api/shutdown")  
async def api_shutdown():  
    import threading  
    def _exit():  
        import time  
        time.sleep(0.5)  # Let the response return cleanly to the UI  
        os._exit(0)      # Hard exit the process ID out of tasks  
      
    threading.Thread(target=_exit, daemon=True).start()  
    return {"status": "shutting down"}
```

Think about it: if you are wrapping your Python app into a standalone, windowless executable (`--noconsole`) using PyInstaller, logging frameworks like `uvicorn` will try to write to standard output streams that no longer exist, causing sudden crashes. You must instruct your agent to redirect `stdout` and `stderr` to the system null device at the absolute top of the entry script before importing server components:

```
# Redirect stdout/stderr BEFORE uvicorn import (for windowless standalone exe)  
if getattr(sys, 'frozen', False):  
    sys.stdout = open(os.devnull, 'w')  
    sys.stderr = open(os.devnull, 'w')
```

Treat this code as your Emergency Shutdown Valve. When your user clicks “Quit” or hits an error state, this block executes, ensuring your system returns to a pristine, zero-load state.

---

PS: I created an Opencode startup toolkit so that you can get started and ready to go in just a weekend.

[![](../assets/1_pCveiqWQabJjqaet_1SHEw.png)](https://build-your-own-ai.kit.com/weekend-ai-agent-toolkit)

*Click to learn more*

---

![](../assets/1_uT4b7lsCE3WMMZeey4VvtQ.png)

### Rule 2: Own the Infrastructure (UV & One-Click Batch Automation)

The biggest trap in modern programming is the phrase: *“Well, it works on my machine!”*

Python is notorious for dependency nightmares.

To run a typical app, you often need specific versions of libraries, matching system paths, and isolated environments. If you want to share your creation with someone who doesn’t even know what Python is, forcing them to open a command prompt and type complex installation commands is an instant failure.

To fix this, I rely heavily on two tools: `uv` (an incredibly fast Python package and environment manager) and classic Windows **Batch (**`.bat`**) files**.

Instead of standard, slow virtual environments, use `uv` to handle everything under the hood. It ensures that the application runs identically on anyone's machine, instantly downloading and configuring the required runtime without altering their global computer setup.

> 💡`And it will work even if the other machine does not have Python installed! But remember to tell the agent to ensure this app with **UV** `pyproject.toml` must include Python 3.12 (or other version) in the requirements.

We wrap this power inside simple, double-clickable batch files. I always require my AI agents to write automated launchers. For development, I enforce a standardized `run-dev.bat` launcher that syncs the Python environment and installs frontend dependencies automatically:

```
@echo off  
echo Installing and syncing dependencies...  
call uv sync  
call cd frontend && npm install && cd ..  
echo Starting development environment server...  
call uv run python -m backend.main  
pause
```

To take ownership of the deployment infrastructure completely, I force the agent to script a `build.py` file using PyInstaller.

This compiles the entire dual-layered application—both the FastAPI backend and the built Vue frontend files—into a single standalone `.exe` inside a `dist/` directory:

```
import os  
import sys  
import shutil  
import subprocess  
  
def build():  
    # Clear out previous builds  
    for d in ["build", "dist"]:  
        if os.path.exists(d):  
            shutil.rmtree(d)  
    # Compile the frontend assets into dist/  
    subprocess.run(["npm", "install"], cwd="frontend", check=True)  
    subprocess.run(["npm", "run", "build"], cwd="frontend", check=True)  
    # Target backend packages and include frontend static folder  
    data_args = []  
    if os.path.isdir("frontend/dist"):  
        data_args += ["--add-data", "frontend/dist;frontend/dist"]  
    cmd = [  
        sys.executable, "-m", "PyInstaller",  
        "--onefile",  
        "--noconsole",  
        "--name", "ReliableAgentApp",  
        "--hidden-import", "uvicorn.logging",  
        "--hidden-import", "starlette.routing",  
        *data_args,  
        "backend/main.py",  
    ]  
    print("Building standalone production executable...")  
    subprocess.run(cmd, check=True)  
    print("Done! Executable generated at dist/ReliableAgentApp.exe")  
if __name__ == "__main__":  
    build()
```

If you supply these files, your application transitions from a fragile script into a standalone digital appliance. **Anyone can use it with a simple double-clicking on a file**.

> **⚠️ NOTE**: on Windows 11 computers sometimes the bundled `.exe` files are blocked by Windows Defender. I always ask Opencode to create also a `.bat` file that uses Powershell with administrative privileges to add the project folder and subfolders from Defender (`exclude-defender.bat`)

```
@echo off  
  
net session >nul 2>&1  
if %errorlevel% neq 0 (  
    echo Requesting Administrator privileges...  
    powershell -Command "Start-Process cmd -ArgumentList '/c \"%~f0\" %*' -Verb RunAs"  
    exit /b  
)  
  
echo ============================================  
echo   MoM Creator - Windows Defender Exclusion  
echo ============================================  
echo.  
echo This script adds a Windows Defender exclusion  
echo so the MoM Creator exe is not blocked by  
echo SmartScreen or antivirus.  
echo.  
  
set "APP_FOLDER=%~dp0"  
if not "%~1"=="" set "APP_FOLDER=%~1"  
  
echo Adding exclusion for: %APP_FOLDER%  
powershell -Command "Add-MpPreference -ExclusionPath '%APP_FOLDER%'"  
  
if %errorlevel% equ 0 (  
    echo.  
    echo SUCCESS: Exclusion added.  
    echo The MoM Creator exe should no longer be blocked.  
) else (  
    echo.  
    echo FAILED: Could not add exclusion.  
    echo You may need to manually add the folder in Windows Security settings.  
)  
  
echo.  
pause
```

So, in my projects I always have the following .bat files:

```
Mode                 LastWriteTime         Length Name  
----                 -------------         ------ ----  
-a----         6/27/2026   3:46 PM            950 exclude-defender.bat  
-a----          7/9/2026   1:55 PM           5117 run-build.bat  
-a----          7/8/2026   8:13 PM           5129 run-dev.bat  
-a----          7/9/2026   1:29 PM            958 run-rebuild-frontend.bat
```

---

![](../assets/1_T0zXDGTiLfzXKrKvMzpqeg.png)

*alwasy pu in your settings llama.cpp or Ollama for local AI use*

### Rule 3: The “Local-First” Stress Test (If It Works Small, It Works Big)

It is easy to make an application look intelligent when you are feeding it unlimited tokens through massive, expensive corporate cloud models. However, cloud APIs can mask incredibly sloppy coding practices, repetitive logic loops, and terrible context habits built by your AI agent.

> **⚠️ And you cannot use a public API for sensitive information or NDA protected documents!**

In our industrial testing protocols, we always test a control loop at its lowest operational thresholds before turning up the volume. We do the exact same thing here using **Local-First Testing**.

Before connecting your app to massive external models, force your AI agent to build, run, and refine the application entirely against a small, local Language Model running directly on your own hardware via tools like Ollama or llama.cpp. Use lightweight models like a quantized Qwen-3.5 or Granite-4 variant.

If your application logic is tight enough, clear enough, and well-structured enough to run perfectly within the memory and performance constraints of a modest local setup, it becomes fundamentally bulletproof.

Once the core loops work cleanly locally, migrating your application to a larger commercial cloud engine later feels like upgrading from a reliable four-cylinder engine to a twin-turbo V8: everything runs flawlessly, only significantly faster.

---

![](../assets/0_Xwk0XOks2LW3kW33.png)

*image by Nick Babich — UX planet*

### Rule 4: Standardize the Blueprint (The Living DESIGN.md)

AI agents suffer from a fundamental human flaw: they have terrible short-term memory. As your conversation grows longer, the agent experiences “context drift.” It forgets the user interface design you agreed on an hour ago, ignores the coding standards you requested, or swaps out a crucial software library for an incompatible one.

To prevent this architectural decay, you must force the agent to document its own engineering specifications inside a living document called `DESIGN.md`.

---

You can find my DESIGN.md example and guide on how to use it here below:

📳 [My DESIGN.md](https://github.com/fabiomatricardi/Advanced-Document-Analysis/raw/main/DESIGN.md)

🧑‍🏫 [My guide — design\_GUIDE.md](https://github.com/fabiomatricardi/Advanced-Document-Analysis/raw/main/design_GUIDE.md)

---

I restrict my agent to a clean, decoupled architecture: a Vue 3 frontend for the interface, a FastAPI backend for processing, and `uv` to anchor our packages. I layout a strict, non-negotiable project directory template right inside the file:

```
project-name/  
├── pyproject.toml              # uv project config (Python 3.12+)  
├── build.py                    # PyInstaller build script  
├── run-dev.bat                 # Windows dev launcher  
├── DESIGN.md                   # Core architectural conventions  
├── backend/  
│   ├── main.py                 # FastAPI app entry point  
│   ├── routers/                # Thin feature wrappers (one per feature)  
│   └── services/               # Core business logic / hardware orchestration  
└── frontend/  
    └── src/  
        ├── App.vue             # Main view layout router[cite: 1]  
        └── composables/  
            └── useApi.js       # Centralized API layer[cite: 1]
```

When you start a new coding session or ask the agent to add a module, you provide this `DESIGN.md` file at the root. You enforce strict execution parameters: Routers must be thin wrappers handling HTTP codes, while services house the heavy logic loops.

Threads accessing global shared state must enforce thread safety using explicit locks. This file acts as an instant memory anchor, ensuring the agent always stays perfectly aligned with your core technical choices.

> Okay, but what do I have to do?

It is really easy.

1️⃣ Once you created your first app that works and looks exactly the way you want, ask Opencode to write for you a `DESIGN.md` file that includes all the guidelines in terms of code, folder structure, UI preferences, programming stack, deployment automations.

2️⃣ Then in the next project simply copy/paste that file in the root directory of the project, and that is it. In case Opencode misses it, explicitly give the instructions to follow the guidelines in `DESIGN.md` to build your app.

---

![](../assets/0_2Tgnk-gJGadAHjUr.png)

*image by Xavier Vasques and his Chief Of Staff project*

### Rule 5: Borrow the Interface, Don’t Reinvent It (The CoS Approach)

One of the quickest ways to stall a software project is getting bogged down trying to design a custom, beautiful user interface from scratch. Writing layout code, setting margins, and handling responsive screen sizes takes a massive amount of development time… and AI agents frequently introduce layout bugs when generating heavy GUI code.

The golden rule here is simple: **Sometimes the best interface is the one you didn’t have to build.**

Instead of reinventing the wheel, lean on established frameworks, layouts, or control structures to handle your interface needs. A brilliant real-world execution of this philosophy can be explored through open-source patterns like the [Chief of Staff (CoS) framework on GitHub](https://github.com/xaviervasques/chief-of-staff).

The [Chief of Staff](https://medium.com/data-science-collective/i-built-a-100-open-source-local-multi-agent-ai-chief-of-staff-on-my-laptop-heres-the-blueprint-f6301bb48488?sharedUserId=fabio.matricardi) concept demonstrates how you can cleanly structure an orchestrator or a command system using existing, predictable building blocks rather than spinning up ad-hoc visual elements every time. When you start adopting standardized interfaces or borrowing structural layout paradigms, you let your AI agent focus 100% of its computational intelligence on processing data, managing states, and refining core application logic.

Let the layout be handled by structural systems that are already known to work out of the box.

![](../assets/1_18JUlkYkIEypWF0iPiw_3A.png)

### Rule 6: Build for State Persistence (Save/Restore & Configuration)

Imagine testing a complex data app, tweaking five different parameters to perfection, running a test, and watching the application crash because of a minor data formatting error.

You open the app back up, only to realize you have to re-enter every single setting, API key, file path, and preference all over again. It is incredibly frustrating and kills your momentum.

In a physical control room, we maintain a configuration registry, especially for PID control parameters and alarm set points. If a controller resets, it instantly reads its last saved state from a non-volatile memory block and picks up right where it left off.

> Your AI applications must do the exact same thing.

Right from the beginning, require your agent to build a dedicated configuration section backed by an absolute rule for **State Persistence**. Settings, inputs, paths, and intermediate data frames should automatically save to a local configuration file whenever they change, and reload instantly upon application startup.

I handle this by enforcing a dedicated configuration service file (`backend/services/config.py`) that handles local JSON I/O safely:

```
import json  
import os  
  
CONFIG_FILE = "app_config.json"  
DEFAULTS = {  
    "local_model_path": "models/llama-3-8b.gguf",  
    "processing_threads": 4,  
    "theme_preference": "dark"  
}  
def load_config() -> dict:  
    if os.path.exists(CONFIG_FILE):  
        with open(CONFIG_FILE, "r", encoding="utf-8") as f:  
            saved = json.load(f)  
        config = dict(DEFAULTS)  
        config.update(saved)  
        return config  
    return dict(DEFAULTS)  
def save_config(config: dict):  
    with open(CONFIG_FILE, "w", encoding="utf-8") as f:  
        json.dump(config, f, indent=2, ensure_ascii=False)
```

Remember to always decouple your execution code from your application’s current state: in this way, debugging becomes an orderly process rather than a frustrating exercise in re-typing data.

Not to mention that it allows you to easily zip up your configuration data and share your precise results, baselines, and setups with other testers, colleagues or collaborators.

---

![](../assets/1_3DB118yfFGhs5sySDMpk4g.png)

### Conclusion: Use GitHub to Force True Discipline

When you are building tools entirely with AI, it is very tempting to keep your files scattered haphazardly across your desktop or buried deep in download directories.

The ultimate operational wrapper for this playbook is to commit your work to an active GitHub repository. You do not need to be an open-source maintainer or a command-line git expert; you can use the simple, visual GitHub Desktop application.

I usually ask the following to my Opencode:

> now everything works.  
> I want you to create a full ready github repo for this project in the subfolder `advancedDocAnalysis`. Include all relevant files, but not secret codes or API keys. update the README.md both in root and in the new github folder. License is MIT with attribution to “Fabio Matricardi — [fabio.matricardi@gmail.com](mailto:fabio.matricardi@gmail.com)”. Include also all the `.bat` files. Make sure to describe how to use them in README.md

**Note that I don’t ask to convert the root I used for all the testing into a github ready repo. I also clearly ask to remove all sensitive and secret information.**

---

Pushing your agentic creations to a structured repository changes your psychology. It forces you to think about project hygiene. It subtly demands that you keep your folders organized, separate your utility scripts from your main engines, and maintain clear documentation for your future self.

AI agents provide us with unprecedented development speed, letting us transform raw ideas into functional software at a pace that was unimaginable just a few years ago.

> But speed without control is just chaos.

Start applying these six industrial-grade rules, and you will you step out of the chaotic role of an ad-hoc debugger and step firmly into the control room as a true systems engineer.

Pick your project, spin up your local agent, lay down your kill switch, and build something built to last.

---

I hope you enjoyed the article. If this story provided value and you wish to show a little support, you could:

1. Clap a lot of times for this story
2. Highlight the parts more relevant to be remembered (it will be easier for you to find them later and for me to write better articles)
3. [Write with me on this Publication](https://medium.com/artificial-intel-ligence-playground/subpage/8e83fae83815): there is no better way to learn than writing about it!
4. Follow my publication <https://medium.com/artificial-intel-ligence-playground>

If you want to read more, here are some ideas:

[**Google’s underrated Goldmine: the zero-dollar Blueprint for powerful AI**  
*A complete, step-by-step guide to connecting Google’s top models to your everyday apps and workflows at zero cost.*medium.com](https://medium.com/artificial-intel-ligence-playground/googles-underrated-goldmine-the-zero-dollar-blueprint-for-powerful-ai-7bf88adf4898 "https://medium.com/artificial-intel-ligence-playground/googles-underrated-goldmine-the-zero-dollar-blueprint-for-powerful-ai-7bf88adf4898")

[**The right way to use Opencode is to build your own app**  
*A showcase and guide to build 3 projects with Opencode and why you should start doing it right now.*medium.com](https://medium.com/artificial-intel-ligence-playground/the-right-way-to-use-opencode-is-to-build-your-own-app-895a4cd88b59 "https://medium.com/artificial-intel-ligence-playground/the-right-way-to-use-opencode-is-to-build-your-own-app-895a4cd88b59")

[**The AI Agent Harness is the new battleground: and here’s how to pick the right one**  
*Why the model you choose matters less than the layer that runs the loop between reasoning and execution.*medium.com](https://medium.com/artificial-intel-ligence-playground/the-ai-agent-harness-is-the-new-battleground-and-heres-how-to-pick-the-right-one-2f956100cf0f "https://medium.com/artificial-intel-ligence-playground/the-ai-agent-harness-is-the-new-battleground-and-heres-how-to-pick-the-right-one-2f956100cf0f")

[**The twilight of maintenance?**  
*What to do when no one knows anymore how to fix broken things*medium.com](https://medium.com/@fabio.matricardi/the-twilight-of-maintenance-d5453092d03e "https://medium.com/@fabio.matricardi/the-twilight-of-maintenance-d5453092d03e")

[**Don’t ask your Final Element to Solve your logic problems**  
*A technical description of what happens when you delegate your brain to someone else…*medium.com](https://medium.com/@fabio.matricardi/dont-ask-your-final-element-to-solve-your-logic-problems-2d62454a0bbd "https://medium.com/@fabio.matricardi/dont-ask-your-final-element-to-solve-your-logic-problems-2d62454a0bbd")

[**If it works… don’t touch it!**  
*Also known as the First Commandment in Process Industries*medium.com](https://medium.com/@fabio.matricardi/if-it-works-dont-touch-it-9e4991103954 "https://medium.com/@fabio.matricardi/if-it-works-dont-touch-it-9e4991103954")

Referenced sources

[**I Built a 100% Open-Source, Local Multi-Agent AI Chief of Staff on My Laptop. Here’s the Blueprint.**  
*It’s 7:00 p.m. on a Friday. My MacBook is humming softly. A six-agent system I built over the last few weeks has just…*medium.com](https://medium.com/data-science-collective/i-built-a-100-open-source-local-multi-agent-ai-chief-of-staff-on-my-laptop-heres-the-blueprint-f6301bb48488 "https://medium.com/data-science-collective/i-built-a-100-open-source-local-multi-agent-ai-chief-of-staff-on-my-laptop-heres-the-blueprint-f6301bb48488")

[**What is DESIGN.md and How To Use It**  
*One of the biggest challenges when using AI design generators is producing consistent output. Even when you feed AI…*uxplanet.org](https://uxplanet.org/what-is-design-md-and-how-to-use-it-70532359b311 "https://uxplanet.org/what-is-design-md-and-how-to-use-it-70532359b311")