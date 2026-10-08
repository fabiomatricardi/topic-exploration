---
post_id: "ae6961d4d12c"
title: "Pick Your Poison: a friendly guide to quantization formats"
subtitle: "The 3 questions that matter (RAM, context length, patience) — Not All Quantizations Are Born Equal part 3"
published: "2026-03-20T15:11:00.570Z"
url: "https://medium.com/@fabio.matricardi/pick-your-poison-a-friendly-guide-to-quantization-formats-ae6961d4d12c"
earnings_usd: 9
---

# Pick Your Poison: a friendly guide to quantization formats

*The 3 questions that matter (RAM, context length, patience) — Not All Quantizations Are Born Equal part 3*

---

![](../assets/1_PSkR-s3IHJUDioicfaLy4w.png)

In [**Part 1**](https://medium.com/artificial-intel-ligence-playground/your-cpu-is-not-broken-the-hidden-truth-about-gguf-quantization-d41a70287a1e), we discovered that your CPU isn’t broken — your quantization format was just wrong. In [**Part 2**](https://medium.com/artificial-intel-ligence-playground/byteshapes-discovery-not-all-bits-are-created-equal-3f5970d0641a), we learned why CPUs hate “smart” IQ formats that GPUs love, thanks to the groundbreaking research at [byteshape.com](https://byteshape.com).

Now comes the million-dollar question:

> ***Okay, I know the theory. Which file do I actually download?***

The internet is full of conflicting advice. Some say “go smallest!” Others say “quality is king!” Everyone has a benchmark, **but nobody has *your* laptop**.

In this article I’m handing you a decision compass.

We’ll cover the three questions that actually matter, the Python scripts to measure your own KPIs, and the exact launch commands to get the best performance out of your i5 or i7.

Let’s stop guessing and start running.

---

By the way, this is part 3 of the series *“Not All Quantizations Are Born Equal”. You can find the entire Series links here*

✅ [Part 1: Your CPU is NOT Broken](https://medium.com/artificial-intel-ligence-playground/your-cpu-is-not-broken-the-hidden-truth-about-gguf-quantization-d41a70287a1e)   
✅ [Part 2: Byteshape’s Discovery: Not All Bits Are Created Equal](https://medium.com/artificial-intel-ligence-playground/byteshapes-discovery-not-all-bits-are-created-equal-3f5970d0641a)  
👉 Part 3: Pick Your Poison: A Friendly Guide to Quantization Formats *(you are here)*  
✅ [Part 4: Llama.cpp optimization for CPU: not all quantizations are born equal](https://medium.com/artificial-intel-ligence-playground/not-all-quantizations-are-born-equal-part-4-llama-cpp-optimization-for-cpu-2e3224aef142)   
- ⏳ Part 5: *The Vulkan Advantage*

---

![](../assets/1_bPcD2wGZcBUddnU_mQVcdA.png)

---

![](../assets/1_H11tnvVFnWLOl9CgrUDhmg.jpeg)

### 🧭 The three questions that actually matter

Forget about bits per weight for a second. To pick the right GGUF format, you only need to answer three questions about your setup and goals.

> And by the end of today article we will create a python app to run the benchmarks in full autonomy for you.

![](../assets/1_4y1wnPqfrzbROJ48b3ppKQ.jpeg)

#### Question 1: How Much RAM Do You Have?

Memory is your hard constraint. If the model doesn’t fit, it doesn’t run (or it swaps to disk, which is painfully slow).

![](../assets/1_pBhwJ_yR_j6EZByxbofrig.png)
> PS: Remember to account for the **KV Cache**. If you plan on long conversations, reserve at least 2–4 GB of RAM for context memory, even with quantized weights.

![](../assets/1_9oLg2bYidzZSOgxxWM31IQ.jpeg)

#### Question 2: How Long Are Your Conversations?

The KV cache is your model’s short-term memory. When you ask a question, the model doesn’t just “know” the answer: it looks back at the conversation so far. To avoid recomputing everything each time, it caches “keys and values” for previous tokens.

> The thing is: **the KV cache is not quantized by default**.

Context length (`-c`) is often overlooked. A 4-bit model with a 32K context can consume more RAM than an 8-bit model with a 4K context.

- **Short prompts (<2K tokens):** Any format works. Focus on speed.
- **Medium chats (4K–8K tokens):** Stick to `Q4_K_M` or `Q5_K_M`.
- **Long documents (>16K tokens):** Avoid extreme quantization (`IQ2_XXS`). The KV cache will dominate your RAM anyway, so you might as well keep the weights high-quality.

If you *must* run long contexts on limited RAM, quantize the KV cache too:

```
.\llama-server.exe -m model.gguf -c 16384 --kv-cache-type q8_0
```

This reduces cache memory usage by ~50% with negligible quality loss.

![](../assets/1_7H4kesIRtreuJFRkO7Yu5Q.jpeg)

#### Question 3: What’s Your Patience Level?

Be honest with yourself.

- **“I need speed”:** You’re chatting casually or testing ideas. Go for `Q4_K_M` or `Q3_K_S`.
- **“I need quality”:** You’re coding, analyzing legal docs, or doing complex reasoning. Go for `Q5_K_M` or `Q6_K`.
- **“I just want it to work”:** Download `Q4_K_M`. It's the community default for a reason.

> **Hot Take**: If you’re unsure, **download the** `Q4_K_M` **version**. You can always go smaller later if you run out of RAM—but you can't un-slow your CPU once you've picked a sluggish format.

### 🐍 Measuring Your Own KPIs (With Python)

Benchmarks in articles are great, but *your* machine is unique. Instead of trusting my numbers, let’s write a simple Python script to measure **Tokens Per Second (TPS)** on your hardware.

This is the same script from Part 1, but now we’ll use it to make a decision. It calls `llama-cli.exe`, runs a prompt, and calculates the speed. No complex libraries needed—just standard Python.

---

![](../assets/1_An4cPknapuMgtWmeUxcZNw.gif)

*the app running on my laptop*

### An app to rule them all

The decision is totally up to you. No one can understand your hardware better than you.

The python app we are going to build is an autonomous script that:

- read all the GGUF in the `models` subfolder
- check your RAM available and the maximum number ot threads available on your CPU
- run a speed test and record the performances
- report back a summary table with the best candidate

The core of the app should be nothing new to you: I used the same snippet from Part 1 of this series, and asked my local Qwen3–4b-instruct to make it prettier and with some more functions (good job… but it took 3 hours).

You can find the code and explanations also in my dedicated GitHub repository here:

[**GitHub - fabiomatricardi/llamacppbenchmarks: a python CLI app to run speed test of GGUF to find the…**  
*a python CLI app to run speed test of GGUF to find the best candidate - fabiomatricardi/llamacppbenchmarks*github.com](https://github.com/fabiomatricardi/llamacppbenchmarks "https://github.com/fabiomatricardi/llamacppbenchmarks")

#### Requirements

1. Python 3.10+ (I am testing it on my windows 11 laptop, with Python 3.12)
2. llama-cli.exe: This script expects the executable to be in the same folder. Donwload the [full binary ZIP archive from llama.cpp](https://github.com/ggml-org/llama.cpp/releases/download/b8287/llama-b8287-bin-win-cpu-x64.zip) un unzip it in the main project directory
3. Dependencies:

```
pip install rich psutil
```

Remember to place your `.gguf` models in a folder (default is `.\models`).

#### The imports and global variables

As usual we import all the libraries we need to call during the execution:

```
import argparse  
import sys  
import psutil  
  
# Try to import rich components  
try:  
    from rich.console import Console  
    from rich.markdown import Markdown  
    from rich.panel import Panel  
    from rich.columns import Columns  
    from rich.text import Text  
    from rich.progress import Progress, TextColumn, BarColumn, TaskProgressColumn, TimeRemainingColumn, TimeElapsedColumn  
    HAS_RICH = True  
except ImportError:  
    HAS_RICH = False  
  
# Fixed prompt  
PROMPT = "explain in simple terms the difference between CPU and GPU during inference"
```

---

![](../assets/1_u19oi_20-paVzGpBwqQdaQ.png)

### 🛠️ Phase 1: the “Hardware Handshake”

Before the app runs a single test, it needs to know what it’s working with. This is where the `psutil` library shines.

```
def get_system_info():  
    ram = psutil.virtual_memory()  
    available_gb = ram.available / (1024 ** 3)  
    max_threads = psutil.cpu_count(logical=True)  
    return round(available_gb, 2), max_threads
```

- **Available RAM:** The function `get_system_info()` checks how much "breathing room" your memory has. This is crucial because loading a model that exceeds your available RAM will cause the benchmark to crawl or crash.
- **The “Thread-Minus-One” Rule:** The app identifies your total CPU threads (e.g., 16) and subtracts one (15). This ensures that while the CPU is “pinned” at 100% during the benchmark, there is still one thread left to keep your mouse moving and your background apps running.

![](../assets/1_rsdJHSmWmmOWRlbSIKGsxg.png)

### 📥 Phase 2: the Command Center (`subprocess`)

The core of the app is the `execute_benchmark` function.

```
def execute_benchmark(folder_path, model_file, thread_count, log_file):  
    model_path = os.path.join(folder_path, model_file)  
    command = [  
        r".\llama-cli.exe", "-m", model_path, "-ngl", "0", "-t", str(thread_count),  
        "--mmap", "-n", "200", "-st", "-p", PROMPT, "-lv", "3",  
        "--reasoning-budget", "0", "--log-file", log_file  
    ]  
    try:  
        result = subprocess.run(command, capture_output=True, text=True, timeout=300, check=False)  
        metrics = extract_speeds_and_bpw(result.stdout, result.stderr)  
        return {  
            "model": model_file, "prompt_speed_tps": metrics["prompt_speed_tps"],  
            "generation_speed_tps": metrics["generation_speed_tps"], "bpw": metrics["bpw"],  
            "output": result.stdout, "error": result.stderr, "returncode": result.returncode  
        }  
    except Exception as e:  
        return {  
            "model": model_file, "prompt_speed_tps": None, "generation_speed_tps": None,  
            "bpw": None, "error": str(e), "returncode": None  
        }
```

Instead of you manually typing commands into a terminal, the script "talks" to `llama-cli.exe` for you.

- **Automation:** It builds a list of arguments (like `-m` for the model path and `-t` for threads) and executes them using `subprocess.run`.
- **The Stopwatch:** We wrap this call in `time.time()` markers. This doesn't just measure the speed of the AI; it measures the **total time** from the moment the model starts loading until it finishes the last word.

![](../assets/1_-vh-jWmwAtuqV0aZvzJc0Q.png)

### 🧪 Phase 3: The “Swiss Army Knife” Regex (`re`)

The most “clever” part of your code is how it reads the AI’s output. `llama-cli` produces a lot of text, but we only want three numbers. We use **Regular Expressions (Regex)** to hunt them down:

- **Prompt Speed:** How fast the AI “reads” your question.
- **Generation Speed:** How fast the AI “writes” the answer.
- **BPW (Bits Per Weight):** This tells the reader how heavily the model was compressed.

The **Regex (Regular Expressions)** section is where the “magic” happens. It’s the part of the code that acts like a digital detective, sifted through thousands of characters of terminal output to find just the three or four numbers we care about.

```
# Regex patterns  
SIMPLE_PROMPT_RE = re.compile(r"Prompt:\s*([\d.]+)\s*t/s")  
SIMPLE_GEN_RE = re.compile(r"Generation:\s*([\d.]+)\s*t/s")  
PROMPT_SPEED_RE = re.compile(r"prompt eval time =.*?(\d+\.\d+)\s*tokens per second")  
GENERATION_SPEED_RE = re.compile(r"eval time =.*?(\d+\.\d+)\s*tokens per second")  
BPW_RE = re.compile(r"file size\s*=\s*[\d.]+ GiB\s*\(\s*([\d.]+)\s*BPW\)")  
  
def extract_speeds_and_bpw(output, error):  
    prompt_speed = gen_speed = bpw = None  
      
    prompt_match = SIMPLE_PROMPT_RE.search(output)  
    if prompt_match: prompt_speed = float(prompt_match.group(1))  
      
    gen_match = SIMPLE_GEN_RE.search(output)  
    if gen_match: gen_speed = float(gen_match.group(1))  
    if prompt_speed is None:  
        detailed_prompt = PROMPT_SPEED_RE.search(output)  
        if detailed_prompt: prompt_speed = float(detailed_prompt.group(1))  
    if gen_speed is None:  
        detailed_gen = GENERATION_SPEED_RE.search(output)  
        if detailed_gen: gen_speed = float(detailed_gen.group(1))  
    bpw_match = BPW_RE.search(error)  
    if bpw_match: bpw = float(bpw_match.group(1))  
    return {"prompt_speed_tps": prompt_speed, "generation_speed_tps": gen_speed, "bpw": bpw}
```

Here is a simple way to explain this.

#### Understanding Regex

Imagine you are handed a 50-page book and told to find every time someone mentions a price in dollars. You wouldn’t read every word; you’d scan for the `$` symbol followed by numbers. That is exactly what a **Regex Pattern** does for our benchmark.

#### 1. The “Flexible” matcher

In our code, we use patterns like this: `r"Prompt:\s*([\d.]+)\s*t/s"`

Let’s “decode” what the computer sees:

- `Prompt:`: Look for this exact word.
- `\s*`: There might be zero or more spaces here (staying flexible!).
- `([\d.]+)`: This is the **Capture Group**. It looks for any combination of digits (`\d`) and decimal points (`.`). The parentheses tell Python: *"Save this specific part for later!"*
- `t/s`: Ensure it’s followed by the unit for "tokens per second."

#### 2. The Fail-Safe logic (the “Fallback”)

One of the most interesting parts of this app is that it doesn’t just have one detective; it has a **backup**.

`llama-cpp` is updated constantly. Sometimes it outputs a clean summary line like `[ Prompt: 7.6 t/s ]`, and other times it outputs a technical log like `prompt eval time = 123.45 ms / 10 tokens (81.00 tokens per second)`.

So we tried to besmart because of this logic:

1. **Try the Simple Pattern:** Scan for the quick summary.
2. **The “If” Check:** If the first detective finds nothing (`is None`), send in the second detective.
3. **The Detailed Pattern:** Scan for the long, technical string.

Without Regex, you would have to use complicated “string slicing” — telling Python to *“go to character 50, then skip 5 spaces, then take the next 4 characters.”* The problem? If the AI’s name is one letter longer, your “slice” breaks. **Regex doesn’t care about position; it cares about patterns.** This makes this app “future-proof” and much harder to break if the output text shifts slightly.

> 🧑‍🏫 look at the `r` before the quotes (e.g., `r"..."`) stands for **"Raw String."** It tells Python: *"Don't try to be clever with backslashes; just treat this text exactly as it is written."* It’s a small detail that makes a huge difference in Regex!

![](../assets/1_mNFTPdcxa88eN8TKkqoTkA.png)

### 🏆 Phase 4: visualizing the Victory (`rich`)

Data is boring if you can’t read it. The final phase turns raw Python dictionaries into a high-end UI.

```
def run_model_in_folder(folder_path, thread_count, log_file="mylog.txt"):  
    models = [f for f in os.listdir(folder_path) if f.endswith(".gguf")]  
    results = []  
  
    if HAS_RICH:  
        progress = Progress(  
            TextColumn("[progress.description]{task.description}"),  
            BarColumn(),  
            TaskProgressColumn(),  
            TimeElapsedColumn(),  
            TimeRemainingColumn(),  
            console=Console()  
        )  
          
        with progress:  
            task = progress.add_task("[cyan]Benchmarking...", total=len(models))  
            for model_file in models:  
                progress.update(task, description=f"🔍 Testing: [bold yellow]{model_file}[/bold yellow]")  
                start_time = time.time()  
                res = execute_benchmark(folder_path, model_file, thread_count, log_file)  
                res["total_duration_sec"] = round(time.time() - start_time, 2)  
                results.append(res)  
                progress.advance(task)  
    else:  
        for model_file in models:  
            start_time = time.time()  
            res = execute_benchmark(folder_path, model_file, thread_count, log_file)  
            res["total_duration_sec"] = round(time.time() - start_time, 2)  
            results.append(res)  
              
    return results
```

- **The Progress Bar:** Using `rich.progress`, we give the user a visual "loading" state. It’s not just a bar; it dynamically updates the text to show exactly which model is currently "under the hood."

```
def print_winners(results):  
    """Identifies and displays the top performing models with corrected alignment and formatting."""  
    if not results or not HAS_RICH:  
        return  
  
    # Filter out N/A values for comparison  
    valid_prompt = [r for r in results if r.get("prompt_speed_tps") is not None]  
    valid_gen = [r for r in results if r.get("generation_speed_tps") is not None]  
  
    best_p = max(valid_prompt, key=lambda x: x["prompt_speed_tps"]) if valid_prompt else None  
    best_g = max(valid_gen, key=lambda x: x["generation_speed_tps"]) if valid_gen else None  
  
    console = Console()  
  
    # 1. Create a grid for the two winner panels  
    grid = Table.grid(expand=True)  
    grid.add_column(ratio=1) # Left side 50%  
    grid.add_column(ratio=1) # Right side 50%  
  
    # 2. Build the Prompt Winner Panel  
    p_panel = ""  
    if best_p:  
        p_text = Text.assemble(  
            ("Prompt King\n", "bold cyan"),   
            (best_p['model'], "yellow"),   
            f"\n{best_p['prompt_speed_tps']} t/s"  
        )  
        p_text.justify = "center" # This is where justify belongs  
        p_panel = Panel(p_text, title="🚀 Fastest Load", border_style="cyan", expand=True)  
  
    # 3. Build the Generation Winner Panel  
    g_panel = ""  
    if best_g:  
        g_text = Text.assemble(  
            ("Generation King\n", "bold green"),   
            (best_g['model'], "yellow"),   
            f"\n{best_g['generation_speed_tps']} t/s"  
        )  
        g_text.justify = "center"  
        g_panel = Panel(g_text, title="✍️ Fastest Gen", border_style="green", expand=True)  
  
    grid.add_row(p_panel, g_panel)  
  
    # 4. Final Print  
    console.print("\n")  
    # Fixed: Removed justify from Panel and used a Text object instead  
    title_text = Text("🏆 BENCHMARK WINNERS", style="bold gold1", justify="center")  
    console.print(Panel(title_text, border_style="gold1", expand=False))  
      
    console.print(grid)
```

- **The Grid Layout:** To fix the alignment issues we encountered, the code uses a `Table.grid`. This forces the "Prompt King" and "Generation King" panels to take up exactly 50% of the screen each, no matter how long the model names are.

---

### How to run it

You can download the [lcpp\_benchmarking.py file clicking here](https://github.com/fabiomatricardi/llamacppbenchmarks/raw/main/lcpp_benchmarking.py).

Open the terminal in the main project folder, and run:

```
python lcpp_benchmarking.py --folder .\your_model_path --output my_results
```

In my example I used it like this:

```
python .\lcpp_benchmarking.py - folder .\models - output results.json
```

---

### Quick tweaks that actually help

Beyond quantization, a few launch flags can squeeze out extra performance on Windows.

#### 1. Thread Count (`-t`)

Don’t use all your logical cores (Hyperthreads). Use your **physical cores** minus 1 or 2 for the OS.  
\* **i5 (6 cores):** Use `-t 4`  
\* **i7 (12 cores):** Use `-t 8` or `-t 10`

#### 2. Memory Mapping (`--mmap`)

This is enabled by default in most builds. It loads the model into virtual memory efficiently. **Keep it on.**

#### 3. Batch Size (`-b`)

For interactive chat, leave this at default (usually 2048). Increasing it helps prompt processing speed but uses more RAM.

> 🧪 Send me your personal experiments results

### 🏁 Series Recap so far — the truth about quantization

We’ve covered a lot of ground over these three weeks. Here’s your cheat sheet:

1. **Smaller ≠ Faster**: Dequantization overhead can make tiny models slower on CPUs (Part 1).
2. **Hardware Matters**: IQ formats are GPU-optimized; KQ formats are CPU-optimized (Part 2).
3. **Pick Wisely**: Use the 3-question decision tree (RAM, Context, Patience) to choose your format (Part 3).

> **“Treat memory as a constraint, not a goal. Once a model fits on your device, what matters is the tradeoff curve: TPS versus quality.”** — [byteshape.com](https://byteshape.com/blogs/Qwen3-30B-A3B-Instruct-2507/)

Don’t chase the smallest file size. Chase the best *experience*.

For 90% of CPU-only users on mid-range hardware, that experience lives in a file named `Q4_K_M.gguf`.

---

#### 🚀 What’s Next?

You now have the knowledge to run local AI efficiently. You know which files to download, how to benchmark them, and how to launch them without melting your laptop.

- [✅ Part 1: Your CPU is NOT Broken *(you are here)*](https://medium.com/artificial-intel-ligence-playground/byteshapes-discovery-not-all-bits-are-created-equal-3f5970d0641a)  
- [✅ Part 2: Byteshape’s Discovery: Not All Bits Are Created Equal](https://medium.com/artificial-intel-ligence-playground/byteshapes-discovery-not-all-bits-are-created-equal-3f5970d0641a)  
- 👉 Part 3: Pick Your Poison: A Friendly Guide to Quantization Formats *(you are here)*  
- ⏳ Part 4: Llama.cpp optimization for CPU: not all quantizations are born equal  
- ⏳ Part 5: *The Vulkan Advantage*

---

I hope you enjoyed the article. If this story provided value and you wish to show a little support, you could:

1. Clap a lot of times for this story
2. Highlight the parts more relevant to be remembered (it will be easier for you to find them later and for me to write better articles)
3. **Join my** [**totally free weekly Substack newsletter here**](https://thepoorgpuguy.substack.com/about)
4. Follow me on Medium
5. Follow my publication <https://medium.com/artificial-intel-ligence-playground>

If you want to read more, here are some ideas:

[**Stop chasing AI benchmarks. Be the Benchmark.**  
*In a world of endless AI releases and shiny leaderboards, the smartest strategy is simple: treat benchmarks as signals…*blog.stackademic.com](https://blog.stackademic.com/stop-chasing-ai-benchmarks-be-the-benchmark-cb483152de45 "https://blog.stackademic.com/stop-chasing-ai-benchmarks-be-the-benchmark-cb483152de45")

[**llama.CPP restyle is the workshop for your Local AI**  
*From LLM routing to full working Chat application: all in one ZIP file. And here is how.*medium.com](https://medium.com/artificial-intel-ligence-playground/llama-cpp-restyle-is-the-workshop-for-your-local-ai-b418d36ced3d "https://medium.com/artificial-intel-ligence-playground/llama-cpp-restyle-is-the-workshop-for-your-local-ai-b418d36ced3d")

[**That blinking cursor just saved your favorite old and blurry photo**  
*How a 30-year-old tech trick (the terminal) is the perfect partner for cutting-edge AI magic*medium.com](https://medium.com/artificial-intel-ligence-playground/that-blinking-cursor-just-saved-your-favorite-old-and-blurry-photo-baa5043d36f6 "https://medium.com/artificial-intel-ligence-playground/that-blinking-cursor-just-saved-your-favorite-old-and-blurry-photo-baa5043d36f6")

[**The power of System messages & Prompt engineering… with open-source models**  
*My modern guide to prompt engineering in generative AI — Part 1*generativeai.pub](https://generativeai.pub/the-power-of-system-messages-prompt-engineering-with-open-source-models-0ca4950f9666 "https://generativeai.pub/the-power-of-system-messages-prompt-engineering-with-open-source-models-0ca4950f9666")

[**The hidden Logic in AI system prompts**  
*My modern guide to prompt engineering in generative AI — Part 2*generativeai.pub](https://generativeai.pub/the-hidden-logic-in-ai-system-prompts-6c91c06b77de "https://generativeai.pub/the-hidden-logic-in-ai-system-prompts-6c91c06b77de")

[**Why your AI reply feels unpredictable (and the simple system that fixes it)**  
*In the end Structured Output is all you need — and here’s how you can do it on your PC*generativeai.pub](https://generativeai.pub/why-your-ai-reply-feels-unpredictable-and-the-simple-system-that-fixes-it-c4adcc70948f "https://generativeai.pub/why-your-ai-reply-feels-unpredictable-and-the-simple-system-that-fixes-it-c4adcc70948f")

[**LFM2: the AI that fits in your pocket and thinks faster than you do**  
*The Liquid AI revolution finally in our hands*generativeai.pub](https://generativeai.pub/lfm2-the-ai-that-fits-in-your-pocket-and-thinks-faster-than-you-do-564e8c9da0b0 "https://generativeai.pub/lfm2-the-ai-that-fits-in-your-pocket-and-thinks-faster-than-you-do-564e8c9da0b0")

#### *Not All Quantizations Are Born Equal — this Series*

[**Byteshape’s discovery: not all bits are created equal**  
*How CPUs and GPUs “think” differently about data*medium.com](https://medium.com/artificial-intel-ligence-playground/byteshapes-discovery-not-all-bits-are-created-equal-3f5970d0641a "https://medium.com/artificial-intel-ligence-playground/byteshapes-discovery-not-all-bits-are-created-equal-3f5970d0641a")

[**Byteshape’s discovery: not all bits are created equal**  
*How CPUs and GPUs “think” differently about data*medium.com](https://medium.com/artificial-intel-ligence-playground/byteshapes-discovery-not-all-bits-are-created-equal-3f5970d0641a "https://medium.com/artificial-intel-ligence-playground/byteshapes-discovery-not-all-bits-are-created-equal-3f5970d0641a")