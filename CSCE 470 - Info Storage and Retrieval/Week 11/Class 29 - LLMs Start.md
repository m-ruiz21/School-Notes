# The plan going forward

- Intro to LLMs
- Looking at the origins of language models.
- Previous how LLMs can help us in search and recommendation.

# Current state of LLMs

Currently we can use LLMs for:
- Simple factoid queries
- Complex and more abstract queries
- Creative outputs like poems.
- Summarization.
- Code understanding.
- Code writing.

**But can we make it recommend?**

# Defining LLMs

First off, what are LLMs?

> Large language models (LLMs) refer to  Transformer language models that contain hundreds of billions (or more) of parameters, which are trained on massive text data. LLMs  exhibit strong capacities to understand natural  language and solve complex tasks (via text generation).

## What is a Transformer?

A transformer is a deep learning architecture proposed in 2017 that relies on the parallel multi-head attention mechanism.

![[Pasted image 20231210175342.png]]

It's the newest and most revolutionary step in Large Language Models.

# AskMSR 
Before we go in depth, let's back up a bit.

Back in the day, whenever we searched up on google, we wouldn't always get a definitive answer, it would give us URLs.

Thus comes **AskMSR**, a question-answering system developed by Microsoft Research.

It consists of the following steps:

## Step 1: Rewrite queries

**Intuition:** The user's question is often syntactically quite close to sentences that contain the answer.

> Where **is the Louvre Museum located**?
> **The Louvre Museum is located** in *Paris* 

But how do we rewrite the queries?

**Solution:** classify the questions into seven categories:
1. Who is/was/are/were ?
2. When is/did/will/are/were ?
3. Where is/are/were ?

From here, create category specific transformation rules.
Like, for "where" questions, move "is" to all possible locations.
## Step 2: Send Rewrites To Search Engine

Send all rewrites to a web search engine and retrieve top N answers.

For speed, rely only on the search engine's "snippets", not the full text of the actual document.

## Step 3: Mining N-Grams

For example, for the text “Web Question Answering: Is More Always Better”:

**Unigrams:** Web, Question, Answering, Is, More, Always, Better.

**Bigrams:** Web Question, Question Answering, Answering Is, Is More, More Always, Always Better.

**Trigrams:** Web Question Answering, Question Answering Is, Answering Is More, Is More Always, More Always Better.

We also create weights for the N-gram: occurrence count, each weighted by the "reliability" (weight) of rewrite that fetched the document.

For example, for the query “Who created the character of Scrooge?”:
- Dickens - 117  
- Christmas Carol - 78  
- Charles Dickens - 75  
- Disney - 72  
- Carl Banks - 54

## Step 4: Filtering N-Grams

Each question type is associated with one or more "data-type filters" = regex. 

We want to boost the score of N-grams that do match regex and lower the score of N-grams that don't match regex.

## Step 5: Tiling the Answers

So combine all the highest-scoring n-grams and repeat until no more overlap.

## Results
So it went into a TREC contest with about 1M documents and 900 questions. 
It didn't 't do too well. Why? because it relies on the enormity of the web!

So, in order for it to be effective, it requires using the Web as the whole.