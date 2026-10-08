---
post_id: "4c1cdedbb3f9"
title: "Maybe keyword search is all you need"
subtitle: "Classic Keyword search is Powerhouse in the right Hands"
published: "2024-02-22T18:17:08.970Z"
url: "https://medium.com/@fabio.matricardi/maybe-keyword-search-is-all-you-need-4c1cdedbb3f9"
earnings_usd: 151
---

# Maybe keyword search is all you need

*Classic Keyword search is Powerhouse in the right Hands*

---

![](../assets/1_ZLpqqTt8_y9IM1heDORHLg.jpeg)

*image by Lexica.art*

While semantic search steals the spotlight with its natural language strength, classic keyword search remains a valuable tool. Maybe it is because Retrieval Augmented Generation became famous, or simply because sometimes is not very clear the user intent… For whatever the reasons it looks like only semantic search is a popular topic.

Has to be really like that? Do you really need all the time a complex search?

---

### What Is the Difference Between Semantic Search and Keyword Search?

Let’s catch with few little definitions, first.

**Keyword Search: a** literal match-based system where searches rely on the exact presence of specific keywords or phrases within the data.

**Semantic Search:** a more sophisticated approach that attempts to understand the meaning and intent behind your query, considering context and relationships between words and concepts.

So, the main difference between semantic search and keyword search is that semantic search focuses on the context and intent behind a search term while a keyword search only matches search records based on the keywords used in the search.

![](../assets/1_4ewiDO5_4fi8PB-2_0tgAQ.png)

*image by the author*

### Maybe all you need is simply a Keyword search

Let’s explore scenarios where the “old-school” method — keyword search shines and the types of data it thrives on.

**1. Precision reigns supreme:** Classic keyword search excels at delivering highly targeted results when you know exactly what you’re looking for. Need a specific document title or a precise phrase? Stringing together the right keywords like pearls on a necklace can deliver pinpoint accuracy.

**2. Simple and clear:** This straightforward approach removes ambiguity. You input keywords, you get results containing those keywords. No room for misinterpretations or unintended associations, making it ideal for tasks like legal research or technical documentation retrieval.

**3. Speed demon:** Due to its reliance on straightforward matching, classic search algorithms process queries faster. This efficiency is crucial for large datasets or applications requiring real-time response, like scientific databases or financial trading platforms.

**4. Control in your hands:** You dictate the search terms, leaving little room for unexpected results. If you enriched your database also with keywords, you can narrow down the search criteria even more. This control is valuable for tasks requiring strict adherence to specific criteria, like regulatory compliance or brand safety checks.

![](../assets/1_9BXL4hiCdeLkCNHXzm47rw.jpeg)

*focus your search*

**5. Structured data paradise:** Classic search flourishes with well-structured data like product catalogs, taxonomies, or metadata-rich databases. Precise keywords can navigate these organized systems with laser focus, providing efficient retrieval of specific information.

**6. Familiar friend:** For users accustomed to traditional search methods, the classic approach offers a comfortable interface. They understand the rules of the game, making it intuitive to find what they need without a learning curve.

**7. Cost-effective option:** Implementing and maintaining classic search infrastructure requires less computational power and resources compared to its semantic counterpart. This makes it a budget-friendly solution for smaller organizations or applications with less complex search needs.

---

### A Proof of Concept — keysearch my articles

So I decided to test it myself!

I went through my 100 articles on Medium, saved them into text files and start building the database. The goal (that may look soo simple…) is to have a search bar that can guide me through all the keywords in my articles and help me find those of my choice.

![](../assets/1_K9Cf6b2P-6r4RP7w5_slUw.png)

*the easy interface*

### Hurdles

First of all I needed to decide what kind of db is required. This is going to be a simple search so a classic database is ok. I opted for a pandas dataframe.

The second thing to consider is the relations in the database: I search for keywords and I want back the chunk of texts that matches the query. But if the same keywords are returning the very same chunk I want only one of it. Let me explain:

My article **A Hitchhiker Guide to LLM with Hugging Face** has many chunks, and any of them have 3 or 4 keywords (for example hitchhiker, llm, guide, ai).

![](../assets/1_ds_jQnQR2LndrhbcVRtmSw.png)

*query run on hitchhiker, llm, huggingface, tutorials*

You can see from the first 2 hits that the document (chunk) is the same, but it refers to two different keywords, indeed requested in the query. The same applies to the third and forth tags (keywords) returning the same document chunk.

We want our results to be unique (if a chunk is already mentioned, we keep only one instance of it)

### How to prepare the data

The data ingestion and processing is the main focus for this task. The good thing is that we can use the steps required to enrich also our RAG strategy.

[**Metadata Metamorphosis: from plain Data to Enhanced insights with Retrieval Augmented Generation**  
*Discover how metadata, the hidden gem of your knowledge base, can be transformed into a powerful tool for enriching…*medium.com](https://medium.com/mlearning-ai/metadata-metamorphosis-from-plain-data-to-enhanced-insights-with-retrieval-augmented-generation-8d1a8d5a6061 "https://medium.com/mlearning-ai/metadata-metamorphosis-from-plain-data-to-enhanced-insights-with-retrieval-augmented-generation-8d1a8d5a6061")

During the data ingestion (our articles) we split them into chunks, and before storing them into LangChain Document format, we run KeyBERT (that is super fast) to extract the keywords of that specific chunk.

Then we add as metadata also the keywords.

> NOTE: this is useful also during RAG because we can run a similarity search combined with a keyword match! 🥳🧠

Next step is to create the database: it will not be a relational db, so we want to have a record for each keyword in every chunk.

Let’s go back to the **hurdle** section: using the same example, the first chunk of the article **A Hitchhiker Guide to LLM with Hugging Face** has 4 keywords (for example hitchhiker, llm, guide, ai). In our database there must be 4 entries for this chunk, one for `hitchhiker`, one for `llm`, one for `guide` and finally one for `ai`.

**The db will become huge!!! Yes but who cares?** Pandas is really efficient and we are going to run an easy keyword match, no complications!

### The Graphic Interface

Must be super simple.

To simplify the search we will use in Streamlit a special widget called multiselect. It is an amazing interactive input widget where you can pass a list of possible choices, you can pick more than one, and you can also start typing and the matches in the existing list will appear.

![](../assets/1_0H0mmN75xQwLHvIJK_GtZQ.png)

*completion of the elements existing in the list*

So one important task is to extract all the keyword tags from the db, removing the duplicates.

```
st.session_state.kwcollection = st.session_state.df['tag'].unique()
```

> In the sidebar you can see that there are 171 unique keywords 👍

The multi-selection object returns a python list. That is good because we can filter the pandas dataframe with the `.isin()` method.

```
dfsearch1 = st.session_state.df[st.session_state.df['tag'].isin(kw)]
```

Where kw is the python list resulting from the multiselect object and `st.session_state.df` is our dataframe (stored into a `session_state` object to be a global variable that not change every Streamlit rerun).

![](../assets/1_VVxZED01DJMcEum_x07OJQ.gif)

*the final result*

### Conclusions

Let me know if you want to see the code behind the scenes. The best it will be for you to try yourself, because refreshing pandas operations is always a good opportunity.

Drop here a comment and in case I will write a follow up 😉

Even though we can see how fast is this type of search strategy… **Remember, classic keyword search isn’t the universal answer.**

For nuanced queries or exploring diverse perspectives, semantic search offers undeniable advantages.

However, when precision, speed, control, and familiarity are paramount, this established method remains a powerful tool in the right hands, especially when paired with well-structured data.

---

Hope you enjoyed the article. If this story provided value and you wish to show a little support, you could:

1. Clap a lot of times for this story
2. Highlight the parts more relevant to be remembered (it will be easier for you to find it later, and for me to write better articles)
3. **Learn how to start to Build Your Own AI**, download [This Free eBook](https://build-your-own-ai.ck.page/97a99ce2f7)
4. Sign up for a Medium membership using [my link](https://medium.com/@fabio.matricardi/membership) — ($5/month to read unlimited Medium stories)
5. Follow me on Medium
6. Read my latest articles <https://medium.com/@fabio.matricardi>

If you want to read more here some ideas:

[**Re-Ranking is All You Need?**  
*Increasing RAG accuracy is not and easy feat: meet LangChain Re-Ranking with Documents pre-processing techniques and a…*medium.com](https://medium.com/artificial-corner/re-ranking-is-all-you-need-7a6b1e586d48 "https://medium.com/artificial-corner/re-ranking-is-all-you-need-7a6b1e586d48")

[**Exploratory Document Analysis… is this a thing?**  
*How to leverage a lighting fast RAG pre-processing LLM building your own AI. All Open-source, all for free.*medium.com](https://medium.com/artificial-corner/exploratory-document-analysis-is-this-a-thing-ed9f4809f364 "https://medium.com/artificial-corner/exploratory-document-analysis-is-this-a-thing-ed9f4809f364")

[**Metadata Metamorphosis: from plain Data to Enhanced insights with Retrieval Augmented Generation**  
*Discover how metadata, the hidden gem of your knowledge base, can be transformed into a powerful tool for enriching…*medium.com](https://medium.com/mlearning-ai/metadata-metamorphosis-from-plain-data-to-enhanced-insights-with-retrieval-augmented-generation-8d1a8d5a6061 "https://medium.com/mlearning-ai/metadata-metamorphosis-from-plain-data-to-enhanced-insights-with-retrieval-augmented-generation-8d1a8d5a6061")

[**Create your LLM API: your ChatBOT as a service — part 1**  
*Master FastAPI and upgrade your LocalGPT to your NetworkGPT*generativeai.pub](https://generativeai.pub/create-your-llm-api-your-chatbot-as-a-service-part-1-4d4213182a1a "https://generativeai.pub/create-your-llm-api-your-chatbot-as-a-service-part-1-4d4213182a1a")

#### [Medium’s Boost](https://medium.com/mlearning-ai/community-mlearning-ai-art-machine-learning-innovators-b81ec864118a) / [AI Life Hacks](https://open.substack.com/pub/mlearning/p/machine-learning-everyday-life-ai-productivity?r=z7zu8&utm_campaign=post&utm_medium=web) / [FREE GPTs alternative](https://open.substack.com/pub/mlearning/p/a-free-alternative-to-the-paid-gpts?r=z7zu8&utm_campaign=post&utm_medium=web) / [AI Art](https://open.substack.com/pub/mlearning/p/ai-art-prompts-analysis-midjourney-alternatives?r=z7zu8&utm_campaign=post&utm_medium=web)

[**Mlearning.ai Submission Suggestions**  
*How to become a writer on Mlearning.ai*medium.com](https://medium.com/mlearning-ai/mlearning-ai-submission-suggestions-b51e2b130bfb "https://medium.com/mlearning-ai/mlearning-ai-submission-suggestions-b51e2b130bfb")