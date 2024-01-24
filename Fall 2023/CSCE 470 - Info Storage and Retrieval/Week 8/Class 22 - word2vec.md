# Recap

Think about how in our methods so far we match a query to a document.

Instead, we'd like to more robustly match a user's search intent. 
That is, we want to understand the query.

# One idea: Query Expansion

Use information on word similarities:
- A manual thesaurus of synonyms for query expansion.
- A measure of word similarity.
	- Calculated from a big document collection
	- Calculated by query log mining (common on the web).


## Thesaurus-based query expansion

For each term t in a query, expand the query with synonyms and related words of t from the thesaurus.

For example: the query "meet me at midnight" -> meet, myself, I, at, night, etc.

This increases recall but lowers precision.

## Another idea: use search engine to help

We can use search engines to find the importance of words to documents retrieved by the search engine. 

# Distributed Representations

Sow we're going to move from "symbolic" representations. With the standard symbolic encoding of terms, each term is a dimension.

So different terms have no inherent similarity:

$$ cat: [0, 0, 0, 0, 0, 1]T$$
$$kitten: [0,0,0,3,0,0] = 0$$

To "distributed" representations where we describe a word based on its properties.

We can find these values by representing a word by the means of its neighbors. 

> This is one of the most successful ideas of modern statistical natural language processing (NLP)

# Solution: Low dimensional vectors

The number of topics that people talk about is small (in some sense)

**Idea:** store the most important information in a fixed small number of dimensions: a dense vector.
> Usually 25-1000 dimensions

So, how can we reduce the dimensionality?
	Go from big, sparse, co-occurrent count vector to low dimensional "word embedding".

So, the goal is to have word meaning be defined in terms of vectors. 

But: **how do we build these dense vectors?**

One of the most important ideas is **word2vec**. So, instead of counting, try to learn the vectors!

# Word2Vec

A framework for learning word vectors.

Big Idea:
- We have a large corpus of text: a long list of words.
- Every word in a fixed vocabulary is represented by a vector
- Go through each position t in text, which has a center word c and context ("outside") words o.
- Use the similarity of the word vectors for c and o to calculate the probability of o given c (or vice versa).
- Keep adjusting the word vectors to maximize this probability.

