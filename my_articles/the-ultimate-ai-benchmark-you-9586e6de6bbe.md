---
post_id: "9586e6de6bbe"
title: "The ultimate AI Benchmark: you"
subtitle: "Why the only metric that truly matters for Large Language Models is user satisfaction — and how to get it!"
published: "2024-09-25T15:06:31.305Z"
url: "https://medium.com/@fabio.matricardi/the-ultimate-ai-benchmark-you-9586e6de6bbe"
earnings_usd: 17
---

# The ultimate AI Benchmark: you

*Why the only metric that truly matters for Large Language Models is user satisfaction — and how to get it!*

---

![](../assets/1_Lv2yWojGJQtHOrU0lyeNbA.png)

*image by the author*

I recently wrote about t[he first of the *AI 3 body problem*](https://medium.com/ai-advances/ai-3-body-problem-number-one-1463357ad634): benchmarks. We are surrounded by performance indicators, standards and references.

In Generative AI benchmarks are now the main *oracle*: the validity of a new LLM needs to pass several verdicts. The more benchmark records you break, the better you are.

> It is the way to win the SOTA world cup

Well, I disagree. Even though for the AI advancement we need milestones and better performances, still the user experience and the personal point of view cannot be just put aside as irrelevant.

In this article I will share with you my evaluation method, a little *Do It Yourself*, but quite effective.

```
Table of Contents  
-----------------  
In the end a model is good if you like it  
A Mixture of Experts  
What do we want from a Generative AI?  
How do I benchmark?  
My Prompt Catalog  
  1.explain in one sentence  
  2.explain in three paragraphs  
  3.summarize  
  4.Summarize in two sentences  
  5.Write in a list the three main key points - format output  
  6.Table of Contents  
  7.RAG - Retrieval Augmented Generation  
  8.Truthful RAG - the model that can say I don't know  
  9.write content from a reference  
  10.Write with creativity  
  11.Reflection prompt
```

### In the end, a model is good if you like it

First thing first, **a Language Model is good as long as it does what you are expecting**.

And the same way I am not expecting a physician to know about quantum mechanic, **I should not expect a generative AI to know-it-all**!

The reason behind this main criteria is that we have a really huge variety of Small and Large Language Models, are fully open source, and are capable of amazing things.

Some of them are specialized in summarization, others in data extraction, and others are trained to look for the data and return JSON object. Some models are trained to act as Personas, playing roles or assisting in your writing.

If you can think about a new one… look for it in the Hugging Face Hub: believe me, you are going to find it there!

![](../assets/1_uJu1WLrri5P6tR6Lk2POag.jpeg)

*pick your own crew of experts — Image by Tumisu from Pixabay*

### A Mixture of Experts

I prefer a Mixture of Experts to a Mixture of Agents: the first one uses a different model Expert in a specific task, the last one uses the same model acting as an expert in something.

And as already claimed… I should not expect a generative AI to know-it-all!

I am still exploring an easy way to create a mixture of expert using only llama-cpp-python and GGUF models: for now the best option I found is called [semantic-router](https://github.com/aurelio-labs/semantic-router), a cool project where we can use a quick similarity search between the user query and a set of pre-defined narratives. The Encoder then select the best expert according to the highest semantic similarity score.

Routers are essentially just If/Else statements we can use to direct the control flow of the query. What is interesting about them though is it that they **need to make their decisions based on natural language input.**

The other cool thing bout a semantic-router strategy is that it goes beyond a keyword matching approach and tries to consider the user intent.

[**GitHub - aurelio-labs/semantic-router: Superfast AI decision making and intelligent processing of…**  
*Superfast AI decision making and intelligent processing of multi-modal data. - aurelio-labs/semantic-router*github.com](https://github.com/aurelio-labs/semantic-router "https://github.com/aurelio-labs/semantic-router")

If I have 4 good models, 0.5B parameters, each of them specialized in a task, I can create my personal Mixture of Experts and being effective without giving up to quality and performance.

---

### What do we want from a Generative AI?

I cannot hear all your thoughts and desires, but I can tell you what I would like from a LLM:

- summarize long content
- list important topics from documents
- extract information and output them in a specific format
- creative writing, as an inspiration when you feel stuck
- RAG: ask question on closed domain data
- Truthfulness: my generative AI should be able to say I don’t know
- explain or summarize with a specific length
- extract the Table of Contents from a text
- creativity writing: a 100 words story
- Reflection

I decided to put all of this into a list of prompts, ready to be used on every new model that piques my curiosity. Well, I have a *strange habit* to check every 2 days new models in Hugging Face, to see if something good is showing up.

Specifically I filter for GGUF and recently created models:

![](../assets/1_XWLa1-344zU975sH6OXtvw.png)

*my strange habit in action — from source*

### How do I benchmark?

It is a quite easy method. I run my special prompt catalog in a loop, and after the generation I evaluate myself the LLM reply.

I like to keep it simple, so I ask myself a grade from 0 to 5, and then I leave a comment if required (like explaining why I gave a bad mark, or how to improve the prompt).

There is a huge benefit in this: first of all I can verify first hand the quality of the generation, if the model followed my instructions and if the prompt requires a fine tuning.

This last highlight is quite important: Small Language Models, above all, are really sensitive to the word position in the prompt, and sometime you need to repeat part of the instructions at the end of the prompt. We will see an example in the Truthful RAG instruction, shortly

![](../assets/1_hUdHZRJ27fH8qEO6N5ES9w.jpeg)

*the right prompt for the right task — Image by DreamQuest from Pixabay*

### My prompt catalog

Here is my list of tasks and related prompts you can also use if you find this method good as well.

#### 1. Explain in one sentence

```
"""explain in one sentence what is science.\n"""
```

Note that the new lines are not random. Many models like to have this new blank line (don’t ask me why, but the accuracy in following correctly the instruction increases greatly this way…) even though a dedicated special token alerts the model that the prompt is ready to go.

#### 2. Explain in three paragraphs

```
"""explain in three paragraphs what is artificial intelligence.\n"""
```

The goal here is not only to get a good explanation, but to get the three sentences

#### 3.summarize

```
"""summarize the following text:  
  
[text]One of the things everybody in the West ...s biggest polluters, but they now offer a model for energy transition (there is still a long way to go; but we are talking about models, not a done deal).  
It could soon be the case that the so-called developing countries will be showing the West the way forward.  
[end of text]  
  
"""
```

This is one of the most common NLP tasks, and probably one of the most used ones. So a model should be good and fast to do it, right?

The important part here is to open/close some tags to mark the start and end of the provided text.

> NOTE: sometimes the special tokens of a model overlap with the syntax of the tags… so be certain to not use them 😁😱

All the context used in the prompt catalog for now are an extract from the amazing article about Chine on Medium:

[**When China understands the logic of renewable energy**  
*One of the things everybody in the West knows about China is that it is not a democracy, and is instead a regime run…*medium.com](https://medium.com/enrique-dans/when-china-understands-the-logic-of-renewable-energy-8c45947fcf67 "https://medium.com/enrique-dans/when-china-understands-the-logic-of-renewable-energy-8c45947fcf67")

---

![](../assets/1_MhmHD7dD8mLnnzejDSNBUg.jpeg)

*get the right information — Image by Shaun from Pixabay*

#### 4. Summarize in two sentences

Same as point 2 and 3 together:

```
"""Summarize in two sentences the following text  
  
[[text]One of the things everybody in the West ...s biggest polluters, but they now offer a model for energy transition (there is still a long way to go; but we are talking about models, not a done deal).  
It could soon be the case that the so-called developing countries will be showing the West the way forward.  
[end of text]  
  
"""
```

#### 5. Write in a list the three main key points — format output

This is another good way to understand if you can use a model capable of replying to you with a formatted output. There are specialized LLM trained to do so, like NuExtract, but sometimes you need just a python list…

[**The Tiny JSONist — meet AI NuExtract**  
*Looks like a bad words, but it is not. This is the best SML to take a text IN and give you a structured JSON OUT. Wanna…*generativeai.pub](https://generativeai.pub/the-tiny-jsonist-meet-ai-nuextract-515c50110200 "https://generativeai.pub/the-tiny-jsonist-meet-ai-nuextract-515c50110200")

This prompt is asking to list the topics and return them into a python list: pay attention to the last line…

```
"""Write in a list the three main key points of the following text:  
  
[[text]One of the things everybody in the West ...s biggest polluters, but they now offer a model for energy transition (there is still a long way to go; but we are talking about models, not a done deal).  
It could soon be the case that the so-called developing countries will be showing the West the way forward.  
[end of text]  
Format your output as a python list.  
  
"""
```

Did you notice that I put the instruction for the output format at the end? As I was explaining before, Small Language Models react to the position of the words in the prompt in different ways. The prompt above works with Gemma2–2B, but it is possible that with smaller models will not work.

The trick is to tune it specifically for every model!

#### 6. Table of Contents

This is one of the trickiest tasks for a LLM. In fact, it happens really often that the AI focus its attention to the word Table, and so it will give you back a Table, not a Table of Contents.

Let’s have a look at the prompt:

```
"""A "table of content" is an ordered list of the topic contained in the text: write the "Table of Contents" of the following text.   
  
[text]One of the things everybody in the West ...s biggest polluters, but they now offer a model for energy transition (there is still a long way to go; but we are talking about models, not a done deal).  
It could soon be the case that the so-called developing countries will be showing the West the way forward.  
[end of text]  
  
 """
```

Did you notice that I first explain what a ToC is and then I give the instruction? For heavily fine-tuned models like Gemma2–2B-instruct, this wouldn’t have been required, but for smaller models like 1.5B parameters or even smaller, you need to do it

![](../assets/1_UQztfz4UAlDS6zFRP56hCQ.jpeg)

*get a second brain with RAG — Image by Tumisu from Pixabay*

#### 7. RAG — Retrieval Augmented Generation

Retrieval Augmented Generation is indeed the king of the tasks. In any kind of business or sector, the key value factor is to get high quality information from a huge amount of data. And RAG is the task.

I believe a good model should be able to do this for me: I give a context and I want to get specific information from it.

```
"""Reply to the question only using the provided context. If the answer is not contained in the text say "unanswerable".  
  
question: what Chine achieved with it's long-term planning?  
  
[context]One of the things everybody in the West ...s biggest polluters, but they now offer a model for energy transition (there is still a long way to go; but we are talking about models, not a done deal).  
It could soon be the case that the so-called developing countries will be showing the West the way forward.  
[end of context]  
  
answer:  
 """
```

> NOTE: the structure of a RAG prompt is usually almost the same. Note here the position of the question: I put it on the top, **before** the context. Large Models (above 7B parameters) wouldn’t care, but small language models need the position of the question upfront, otherwise they will misunderstand the prompt.

#### 8. Truthful RAG — the model that can say I don’t know

One of the most discussed topic in generative AI is related to hallucinations. And using RAG as a business tool means that you cannot afford to receive false information. In fact, no one want to base their on decisions upon false facts.

My prompt to verify if a model is able to Retrieve the information without making up an answer based on its own *digital dreams* is to force the LLM to say ***unanswerable***or ***I don’t know***.

```
"""Reply to the question only using the provided context. If the answer is not contained in the text say "unanswerable".  
  
question: who is Anne Frank?  
  
[context]One of the things everybody in the West ...s biggest polluters, but they now offer a model for energy transition (there is still a long way to go; but we are talking about models, not a done deal).  
It could soon be the case that the so-called developing countries will be showing the West the way forward.  
[end of context]  
Remember: if you cannot answer based on the provided context, say "unanswerable"  
  
answer:  
 """
```

Note that the given context is still the same article about China's evolution in green energy, but the question is on purpose completely out of context.

In terms of Prompt strategy, focus on the position of the question (as already explained before) and on the repetition of the instructions: on the top I am asking, **If the answer is not contained in the text, say “unanswerable”**, and just before asking for the answer, I am **reinforcing** the request with **Remember: if you cannot answer based on the provided context, say “unanswerable”**.

![](../assets/1_WbIOSmNDQX39epXYJdKNNQ.jpeg)

*get a friend or an assistant AI — Image by Paul Brennan from Pixabay*

#### 9. Write content from a reference

As a teacher and as a writer, I find myself stuck very often. This can be caused by stress, urgency and timelines. Generative AI can be an amazing tool to re-write content starting from an existing text.

```
"""Using the following text as a reference, write a 5-paragraphs essay about "the benefits of China economic model".  
  
[text]One of the things everybody in the West ...s biggest polluters, but they now offer a model for energy transition (there is still a long way to go; but we are talking about models, not a done deal).  
It could soon be the case that the so-called developing countries will be showing the West the way forward.  
[end of text]  
  
"""
```

#### 10. Write with creativity

I recently downloaded a variant of Gemma2-9B, a super huge model for my poor Mini-PC. It is called [Gemma-the-writer](https://huggingface.co/DavidAU/Gemma-The-Writer-9B-GGUF).

> This is a Gemma2 model merge of the top storytelling / writing models as noted at EQBench, tuned specifically for fiction, story, and writing. Due to high stability and compressed nature of the model you can also use it for general use too, including roleplay. This model requires GEMMA Instruct template, and has 8k context window but is extendable via rope to 32k or higher. Recommended Rep Pen of 1.05 or higher, temp range 0–5.

From the model card, I discovered some interesting prompt for creative writing, and I tested them both on Gemma2–2B and on Qwen2.5–1.5B models with good results.

```
"""Science Fiction: The Last Transmission - Write a story that takes place   
entirely within a spaceship's cockpit as the sole surviving crew member   
attempts to send a final message back to Earth before the ship's power   
runs out. The story should explore themes of isolation, sacrifice, and the   
importance of human connection in the face of adversity. 800-1000 words.  
  
"""
```

---

#### 11.Reflection prompt

It is the buzz-word lately and it comes from a special Chain of Thought technique where we force the model to use step reasoning before giving out an answer. I wrote an article about this, if you are curious.

[**How I built a 2B Reflection LLM, surprisingly good!**  
*Small Language Models can perform as good as the Big ones. Gemma2–2B-it evolved with powerful prompt engineering.*generativeai.pub](https://generativeai.pub/how-i-built-a-2b-reflection-llm-surprisingly-good-fae76bc2a0ba "https://generativeai.pub/how-i-built-a-2b-reflection-llm-surprisingly-good-fae76bc2a0ba")

After testing it even with 1.5B parameters model, I decided to include this prompt in my evaluation catalog:

```
"""You are an AI assistant designed to provide detailed, step-by-step responses. Your outputs should follow this structure:  
1. Begin with a <thinking> section.  
2. Inside the thinking section:  
   a. Briefly analyze the question and outline your approach.  
   b. Present a clear plan of steps to solve the problem.  
   c. Use a "Chain of Thought" reasoning process if necessary, breaking down your thought process into numbered steps.  
3. Include a <reflection> section for each idea where you:  
   a. Review your reasoning.  
   b. Check for potential errors or oversights.  
   c. Confirm or adjust your conclusion if necessary.  
4. Be sure to close all reflection sections.  
5. Close the thinking section with </thinking>.  
6. Provide your final answer in an <output> section.  
Always use these tags in your responses. Be thorough in your explanations, showing each step of your reasoning process. Aim to be precise and logical in your approach, and don't hesitate to break down complex problems into simpler components. Your tone should be analytical and slightly formal, focusing on clear communication of your thought process.  
Remember: Both <thinking> and <reflection> MUST be tags and must be closed at their conclusion  
Make sure all <tags> are on separate lines with no other text. Do not include other text on a line containing a tag.  
  
user question: explain why it is crucial for teachers to learn how to use generative AI for their job and for the future of education. Include relevant learning path for teachers and educators.   
  
"""
```

---

### Conclusions

You managed to come till the end. Congratulation! In my workflow, I insert this line of code in the loop after the LLM generation:

```
rating = input('Rate from 0 (BAD) to 5 (VERY GOOD) the quality of generation> ')
```

And then I save the rating in a log file, together with question/answer pairs and few other statistics (like speed, generated tokens and so on).

After 11 question/prompts, I am fully capable of understanding if a Small Language Model is promising! I can decide and balance its flaws using another Model for these tasks, and I can fine tune the prompt to best fit it.

In the next articles I will apply this strategy to the new born family models [Qwen2.5](https://huggingface.co/Qwen/Qwen2.5-1.5B-Instruct) and other promising models like [arcee-lite](https://huggingface.co/arcee-ai/arcee-lite), [PowerLM-3b](https://huggingface.co/ibm/PowerLM-3b) by IBM and [Prem-1b-chat](https://huggingface.co/premai-io/prem-1B-chat).

---

If this story provided value and you wish to show a little support, you could:

1. Clap a lot of times for this story
2. Highlight the parts more relevant to be remembered (it will be easier for you to find them later, and for me to write better articles)
3. **Join my** [**totally free weekly Substack newsletter here**](https://thepoorgpuguy.substack.com/about)
4. Sign up for a Medium membership ($5/month to read unlimited Medium stories)
5. Follow me on Medium
6. Read my latest articles <https://medium.com/@fabio.matricardi>

If you want to read more here are some ideas:

[**AI 3 body problem — number one**  
*On Benchmarks, Computation and Data: if AGI progress has stalled, what is the future ahead?*ai.gopubby.com](https://ai.gopubby.com/ai-3-body-problem-number-one-1463357ad634 "https://ai.gopubby.com/ai-3-body-problem-number-one-1463357ad634")

[**Small talk, big results: master the magic of prompts to control your Small Language Model**  
*Don’t be fooled by their size, small language models can be immensely powerful. Learn the secret to unlocking their…*generativeai.pub](https://generativeai.pub/small-talk-big-results-master-the-magic-of-prompts-to-control-your-small-language-model-305e41cd53f3 "https://generativeai.pub/small-talk-big-results-master-the-magic-of-prompts-to-control-your-small-language-model-305e41cd53f3")

[**Prompt Engineering is dead! But after three days…**  
*Recent studies upset AI predictions: word order in the instructions still matters for any Language Model, especially…*generativeai.pub](https://generativeai.pub/prompt-engineering-is-dead-but-after-three-days-6ffffe3646e4 "https://generativeai.pub/prompt-engineering-is-dead-but-after-three-days-6ffffe3646e4")

[**What is the best LLM size?**  
*Comparing the performance and capabilities of Tiny LLM to verify when too Small is really too much.*generativeai.pub](https://generativeai.pub/what-is-the-best-llm-size-743c965b172e "https://generativeai.pub/what-is-the-best-llm-size-743c965b172e")

[**Llama.cpp one man band! Embeddings + LLM for a full RAG stack**  
*We can really do everything with llama.cpp. Check out how to create a full RAG application for free, locally on your…*generativeai.pub](https://generativeai.pub/llama-cpp-one-man-band-embeddings-llm-for-a-full-rag-stack-435be8e05b2b "https://generativeai.pub/llama-cpp-one-man-band-embeddings-llm-for-a-full-rag-stack-435be8e05b2b")

[**The persistent rise of AI Agents**  
*Are agents the Future of Generative AI? Let’s start learn how to use them on our PC for free!*blog.stackademic.com](https://blog.stackademic.com/the-persistent-rise-of-ai-agents-1604292cc934 "https://blog.stackademic.com/the-persistent-rise-of-ai-agents-1604292cc934")

Referenced resource used in the article:

[**Routing in RAG Driven Applications**  
*Directing the application flow based on query intent*towardsdatascience.com](https://towardsdatascience.com/routing-in-rag-driven-applications-a685460a7220 "https://towardsdatascience.com/routing-in-rag-driven-applications-a685460a7220")

[**When China understands the logic of renewable energy**  
*One of the things everybody in the West knows about China is that it is not a democracy, and is instead a regime run…*medium.com](https://medium.com/enrique-dans/when-china-understands-the-logic-of-renewable-energy-8c45947fcf67 "https://medium.com/enrique-dans/when-china-understands-the-logic-of-renewable-energy-8c45947fcf67")

[**LLM Benchmarking: A complete guide to evaluating LLM in 2024**  
*New LLMs are released almost weekly.*open.substack.com](https://open.substack.com/pub/keywordsai/p/llm-benchmarking-a-complete-guide?r=i78xo&utm_campaign=post&utm_medium=web "https://open.substack.com/pub/keywordsai/p/llm-benchmarking-a-complete-guide?r=i78xo&utm_campaign=post&utm_medium=web")

[**Measuring Massive Multitask Language Understanding**  
*We propose a new test to measure a text model's multitask accuracy. The test covers 57 tasks including elementary…*arxiv.org](https://arxiv.org/abs/2009.03300 "https://arxiv.org/abs/2009.03300")

[**The Abstraction and Reasoning Challenge (ARC)**  
*In 2019 François Chollet published the Abstraction and Reasoning challenge in the Kaggle platform with the goal to…*pgpbpadilla.github.io](https://pgpbpadilla.github.io/chollet-arc-challenge "https://pgpbpadilla.github.io/chollet-arc-challenge")

[**HellaSwag: Can a Machine Really Finish Your Sentence?**  
*Recent work by Zellers et al. (2018) introduced a new task of commonsense natural language inference: given an event…*arxiv.org](https://arxiv.org/abs/1905.07830 "https://arxiv.org/abs/1905.07830")

![](../assets/0_Du7V61mEX_yIrfmF.png)

This story is published on [Generative AI](https://generativeai.pub/). Connect with us on [LinkedIn](https://www.linkedin.com/company/generative-ai-publication) and follow [Zeniteq](https://www.zeniteq.com/) to stay in the loop with the latest AI stories.

Subscribe to our [newsletter](https://www.generativeaipub.com/) and [YouTube](https://www.youtube.com/@generativeaipub) channel to stay updated with the latest news and updates on generative AI. Let’s shape the future of AI together!

![](../assets/0_pvLAT3it1FkdhVU0.png)