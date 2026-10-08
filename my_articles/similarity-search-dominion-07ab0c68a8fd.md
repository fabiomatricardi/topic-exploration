---
post_id: "07ab0c68a8fd"
title: "Similarity Search dominion"
subtitle: "From recommendation systems to Retrieval Augmented Generation: the real engine for an AI application."
published: "2024-03-13T04:16:43.997Z"
url: "https://medium.com/@fabio.matricardi/similarity-search-dominion-07ab0c68a8fd"
earnings_usd: 11
---

# Similarity Search dominion

*From recommendation systems to Retrieval Augmented Generation: the real engine for an AI application.*

---

![](../assets/1_T1pM4DBV9qxRBFnHDH_ZoQ.png)

*modified by the author — original Image by Monika from Pixabay*

Semantic Search and Question Answering are the first practical use cases for AI application. Why?

In principle because we are still used to the good old Google Search bar approach to problem solving: I ask Google. Following up is because everyone need help for something practical… and the easiest why is (and it has always been) to ask questions.

But let’s start from the beginning…

```
What is Semantics  
What is Semantic Search  
Why is semantic search important?  
  1.The words in your head might not perfectly match what you find online.  
  2.Confusing searches? Blame those tricky words!  
  3.The need to understand word Families and to spot People, Places & More  
  4.Your personal interests matter  
Sentence Transformers
```

### What is Semantics

We all know what is Search… but semantic?

Semantics, often referred to as linguistic semantics, is the branch of linguistics that studies the meanings of words, phrases, and sentences in a language. It explores how meaning is derived, how words acquire their meanings, and how these meanings relate to each other within expressions. Semantics distinguishes between sense (the ideas or concepts associated with an expression) and reference (the object or idea denoted by the expression).

At the initial development of the Artificial Intelligence, the study of the words, language and semantics has been an essential component. The concept of connecting AI with semantics dates back to the 1950s when researchers such as Alan Turing were interested in developing machines that could understand and generate natural language. Turing’s famous Turing Test, where a computer must be indistinguishable from a human in a natural language conversation, reflects this early interest in semantics for AI.

![](../assets/0__x1pS3w3Po39oiSx.png)

In the 1960s and 1970s, AI researchers focused on developing algorithms that could process natural language data, known as natural language processing (NLP) or computational linguistics. This included work on parsing, syntax analysis, and natural language understanding (NLU). The creation of machine learning algorithms that could learn from linguistic data also became important during this time.

Natural language processing (NLP) is the study of computers that can understand human language, and refers to the intersection of both AI and linguistics. Today, AI continues to integrate with semantics through natural language processing (NLP) capabilities that allow computers to understand and generate human languages, understanding the relationships between words and concepts. This enables AI systems to perform tasks such as sentiment analysis (detecting emotions or attitudes towards something), topic modeling (identifying patterns or topics within text), machine translation (converting text from one language to another), and more.

---

### What is Semantic Search

We can start with a temporary definition:

> ***Semantic search*** *is a fancy way of saying that when you do a web search, the search engine doesn’t just look for exact matches of words in your query. It tries to understand your intention and the overall meaning of the words you used. This can make the results more relevant to you.*

To understand it better, let’s check out few examples

Have you ever noticed that Bing, Google and other Search Engines can handle almost any question you throw at it these days? Just look at the result for this query:

![](../assets/0_VCoqROrDD70G-Bb9.png)

Despite not mentioning at all Groot by name, Bing was able to understand who we were talking about, and what we wanted to know about him. This wouldn’t be possible without semantic search.

### Finally… what is semantic search?

Semantic search is an information retrieval process used by modern search engines to return the most relevant search results. It focuses on the **meaning** behind search queries instead of the traditional keyword matching.

So primarily Semantic search is concerned only about the meaning and intention behind the words… and this means that it is now clear why Semantics is so important also in Artificial Intelligence.

![](../assets/1_hUdHZRJ27fH8qEO6N5ES9w.jpeg)

*Image by DreamQuest from Pixabay*

If you want to see in actions semantic search you can read more here:

[**Strange Case of Dr Cosine and Mr Relevance**  
*The never ending dilemma between similarity and relevance, Semantic Similarity Search and hard work in curating our…*generativeai.pub](https://generativeai.pub/strange-case-of-dr-cosine-and-mr-relevance-8bc89690ff7f "https://generativeai.pub/strange-case-of-dr-cosine-and-mr-relevance-8bc89690ff7f")

### Why is semantic search important?

Although there are countless variables at play, the principles of semantic search, why it’s needed, and how it’s influenced are easy to understand.

1. The words in your head might not perfectly match what you find online.
2. Confusing searches? Blame those tricky words!
3. The need to understand word Families and to spot People, Places & More
4. Your personal interests matter

Let’s check them one by one.

#### 1. The words in your head might not perfectly match what you find online.

Even worse, we sometimes don’t even know how to articulate a search query properly.

Imagine you’re looking for something online, but you can’t quite find the right words to describe it. That’s where semantic search comes in! Here’s the basic idea:

- People don’t always search for things using the exact same words websites use.
- Sometimes we just can’t think of the perfect words to describe what we’re looking for.
- Think about that catchy song you heard on the radio. You couldn’t remember the title or artist, so you had to search for it using random lyrics until you finally found it!

Semantic search helps search engines understand what you really mean, even if your search terms aren’t perfect.

![](../assets/0_JKmTcuGjY7h26a9z.png)

*one of my favorite songs…*

There are just so many ways to express the same idea, and search engines need to deal with all of them. They need to be able to match the content in their index with your search query based on the meaning of both.

However challenging this may sound already, it’s just the beginning.

#### 2. Confusing searches? Blame those tricky words!

Have you ever searched for something online and gotten results that weren’t quite what you expected? It’s not your fault! Turns out, many words have multiple meanings, kind of like a chameleon can change colors. This makes searching tricky for computers.

Let’s take the word “python” for example. It can mean:

- A cool programming language used to build websites and games (think the brains behind your favorite online stuff).
- A long, slithery snake (the kind you might see in a zoo).
- A hilarious comedy group from Britain (if you’re a Monty Python fan, you know what’s up!).

![](../assets/0_1J1n7YwJQLcmX2HA.png)

The problem is, computers need a little help figuring out which “python” you actually mean. They rely on things like the other words in your search and what people usually search for with that word.

There are even words that can be nouns, verbs, or adjectives all at once! And forget about sarcasm — that’s a whole other level of tricky for computers to understand.

The key thing to remember is that understanding the context of your search is super important. That’s what the next part will be all about!

If you’re a tech whiz, you probably think of the awesome programming language used to build websites and games. But for others, “python” might mean the scary snake slithering in the zoo or the wacky comedy group that makes them laugh.

That’s the challenge! Words can be like puzzle boxes with hidden meanings. Here’s why computers get confused:

- **Double (or Triple!) Duty Words:** Many words, like “bat” (the flying mammal or a baseball tool), can be nouns, verbs, or both!
- **Beyond the Literal:** Sometimes, words have hidden meanings, like sarcasm. Imagine searching for “amazing movie” but secretly hating it — computers might miss that!

Context is everything in semantics, and it brings us to the remaining two points.

#### 3. The need to understand word Families and to spot People, Places & More

Let’s take a look at the following search query and the top search result:

![](../assets/0_eCyLBaBghPBiYv2U.png)

That’s truly impressive. Here’s what Google has to do to understand this query:

1. Know that father refers to the actor, not to the character (otherwise we should have gotten Jackie Chan…).
2. Understand that there is an old and a new Karate Kid.
3. Make the connections.
4. Display search results in a way that shows these connections

I can’t even imagine what kind of search results I’d get if I did that search 15 years ago or earlier.

Now, let’s take a step back to explain the concepts.

- Words have **connections**, like a family tree.
- As mentioned earlier, our queries often don’t match the exact wording of the desired content. Knowing that “affordable” is anything between cheap, mid-range, and reasonably priced is crucial.
- **Entities**, in this example, are movie and series characters (Karate Kid), people with a specific job (actor), and people who are associated with them (father and son). In general, entities are objects or concepts that can be distinctly identified — often people, places, and things.

---

Phew! Language can be tricky, but that’s what makes semantic models so cool — they can understand the complexities and still get you the answers you need!

And as if all the language intricacies weren’t enough, we must go even beyond that.

![](../assets/0_EDxHcu3cQPIwqvyI.png)

#### 4. Your personal interests matter

Let’s go back to the “python” example. If I search for this, I do indeed get all results related to the programming language.

No matter how much we dislike all the ways our personal data is used, it’s at least useful for search engines. Google uses limited data together with your search history to deliver more accurate and personalized search results.

At the core of this complex operation in the background there is BERT. Bidirectional Encoder Representations from Transformers (BERT) is an AI model developed by Google used for natural language processing tasks and particularly good at understanding language in its context (bidirectionally).

Today the most powerful models for semantic search are the Sentence Transformers family.

### Sentence Transformers

[SentenceTransformers](https://huggingface.co/sentence-transformers) 🤗 is a Python framework for state-of-the-art sentence, text and image embeddings.

This library came to light as a result of the studies and researched outlined in the famous paper [**Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks**](https://arxiv.org/abs/1908.10084).

![](../assets/0_aOUGYk1SvZbajFa0.png)

#### The Past…

BERT and RoBERTa has set a new state-of-the-art performance on sentence-pair regression tasks like semantic textual similarity (STS). However, it requires that both sentences are fed into the network, which causes a massive computational overhead: Finding the most similar pair in a collection of 10,000 sentences requires about 50 million inference computations (~65 hours) with BERT.

#### The Present…

> We present Sentence-BERT (SBERT), a modification of the pretrained BERT network that use siamese and triplet network structures to derive semantically meaningful sentence embeddings that can be compared using cosine-similarity. This reduces the effort for finding the most similar pair from 65 hours with BERT / RoBERTa to about 5 seconds with SBERT, while maintaining the accuracy from BERT.  
> We evaluate SBERT and SRoBERTa on common STS tasks and transfer learning tasks, where it outperforms other state-of-the-art sentence embeddings methods.

You can use this framework to compute sentence / text embeddings for more than 100 languages. These embeddings can then be compared e.g. with cosine-similarity to find sentences with a similar meaning. This can be useful for semantic textual similarity or semantic search.

> Embeddings should not be anymore a secret to you right? In case you missed read more here:

[**Strange Case of Dr Cosine and Mr Relevance**  
*The never ending dilemma between similarity and relevance, Semantic Similarity Search and hard work in curating our…*generativeai.pub](https://generativeai.pub/strange-case-of-dr-cosine-and-mr-relevance-8bc89690ff7f "https://generativeai.pub/strange-case-of-dr-cosine-and-mr-relevance-8bc89690ff7f")

[**Maybe Embeddings Are What You Need**  
*A beginner’s guide to understanding embeddings in Machine Learning and how they bridge the gap in NLP.*ai.plainenglish.io](https://ai.plainenglish.io/maybe-embeddings-are-what-you-need-1506d1a07d0f "https://ai.plainenglish.io/maybe-embeddings-are-what-you-need-1506d1a07d0f")

The idea behind semantic search is to embed all entries in your corpus, whether they be sentences, paragraphs, or documents, into a vector space. At search time, the query is embedded into the same vector space and the closest embeddings from your corpus are found. These entries should have a high semantic overlap with the query.

But this will open a complete new chapter! And we will continue it next time…

---

### Conclusions

So, how do we actually use Sentence Transformers for Semantic Search? Stay tuned for the next article, with hands on real life code examples.

Hope you enjoyed the article. If this story provided value and you wish to show a little support, you could:

1. Leave your claps for this story
2. Highlight the parts that you feel are more relevant, and worth remembering (it will be easier for you to find them later, and for me to write better articles)
3. **Learn how to start to Build Your Own AI**, download [This Free eBook](https://build-your-own-ai.ck.page/97a99ce2f7)
4. Follow me on Medium
5. Read my latest articles: <https://medium.com/@fabio.matricardi>

If you want to read more, here are some ideas:

[**Smarter, not Bigger — 1 Million token context is not all you need!**  
*Open source at the test bench to verify long context information extraction. Are they really that good?*medium.com](https://medium.com/@fabio.matricardi/smarter-not-bigger-1-million-token-context-is-not-all-you-need-e9832ba9df66 "https://medium.com/@fabio.matricardi/smarter-not-bigger-1-million-token-context-is-not-all-you-need-e9832ba9df66")

[**Home Acceptance Test for Small Language Models**  
*Create your Home Lab to test the chatbot capabilities of the newest Small Language Models.*blog.stackademic.com](https://blog.stackademic.com/home-acceptance-test-for-small-language-models-57d098c8e094 "https://blog.stackademic.com/home-acceptance-test-for-small-language-models-57d098c8e094")

[**Maybe keyword search is all you need**  
*Classic Keyword search is Powerhouse in the right Hands*medium.com](https://medium.com/@fabio.matricardi/maybe-keyword-search-is-all-you-need-4c1cdedbb3f9 "https://medium.com/@fabio.matricardi/maybe-keyword-search-is-all-you-need-4c1cdedbb3f9")

[**Strange Case of Dr Cosine and Mr Relevance**  
*The never ending dilemma between similarity and relevance, Semantic Similarity Search and hard work in curating our…*generativeai.pub](https://generativeai.pub/strange-case-of-dr-cosine-and-mr-relevance-8bc89690ff7f "https://generativeai.pub/strange-case-of-dr-cosine-and-mr-relevance-8bc89690ff7f")

#### Resources:

[**Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks**  
*BERT (Devlin et al., 2018) and RoBERTa (Liu et al., 2019) has set a new state-of-the-art performance on sentence-pair…*arxiv.org](https://arxiv.org/abs/1908.10084 "https://arxiv.org/abs/1908.10084")

[**Understanding Semantic Search and Question Answering**  
*In this article, we explain key concepts and terminology of semantic (or 'neural') search and question answering…*www.deepset.ai](https://www.deepset.ai/blog/understanding-semantic-search "https://www.deepset.ai/blog/understanding-semantic-search")

[**Ontology (information science) - Wikipedia**  
*In information science, an ontology encompasses a representation, formal naming, and definitions of the categories…*en.wikipedia.org](https://en.wikipedia.org/wiki/Ontology_%28information_science%29 "https://en.wikipedia.org/wiki/Ontology_(information_science)")

[**What Is Semantic Search? How It Impacts SEO**  
*Semantic search is an information retrieval process used by modern search engines to return the most relevant search…*ahrefs.com](https://ahrefs.com/blog/semantic-search/ "https://ahrefs.com/blog/semantic-search/")

[**NLP Resources | Haystack**  
*Some resources to get going with NLP.*haystack.deepset.ai](https://haystack.deepset.ai/nlp-resources "https://haystack.deepset.ai/nlp-resources")

### Stackademic 🎓

Thank you for reading until the end. Before you go:

- Please consider **clapping** and **following** the writer! 👏
- Follow us [**X**](https://twitter.com/stackademichq) **|** [**LinkedIn**](https://www.linkedin.com/company/stackademic) **|** [**YouTube**](https://www.youtube.com/c/stackademic) **|** [**Discord**](https://discord.gg/in-plain-english-709094664682340443)
- Visit our other platforms: [**In Plain English**](https://plainenglish.io) **|** [**CoFeed**](https://cofeed.app/) **|** [**Venture**](https://venturemagazine.net/) **|** [**Cubed**](https://blog.cubed.run)
- More content at [**Stackademic.com**](https://stackademic.com)