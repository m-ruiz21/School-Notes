# Recall: Scoring as the basis of ranking

Recall the simple [[Class 07 - Ranking Functions|scoring functions]] $score(q,d)$ we have created: 
$$score(q,d)= cosine(q,d) = BM25(q,d)$$
Also recall the brainstorming of other ranking factors:
- **YouTube**: views, subscribers, video length, title relevance, etc.
- **LinkedIn**: popularity of job posting, number of openings, recency, etc.

## Different kinds of features

When we think of features we want to add to the scoring function, there's three types of features we can group them in: 
- **Query-independent (or static)**: Depend only on the document (not the query).
	- For example, number of listens to a song in the past month.
- **Query-dependent**: Depend on both the document and the query.
	-  For example, cos similarity or BM25.
- **Query-level**: Depends only on the query (not the document).
	- For example, number of words in query.

## From one ranking factor to many factors.
So this allows us to take one ranking factor to many factors. For example:

$$score(q,d) = a_1 * cos(q,d) + a_2 * BM25 * a_3 * popularity(d)$$ 
In practice, there's feature engineers that go out and discover the features to add and tweak their importance or emphasis by hand.

Instead of doing this, we can **learn** a good ranking algorithm using Machine Learning (ML).

# Learning a ranking algorithm
## Brief background: Learning Tasks

- **Regression**: trying to predict a real value.
- **Binary classification**: trying to predict a simple yes/no response.
- **Multiclass classification**: trying to put an example into a number of classes. 
- **Ranking**: put set of objects in order of relevance.

## How do we learn the function f?

Typically, we will rely on training data that has the correct outputs / known labels.
Specifically we'll have the data split into a **training set** and a **test set**.

## ML + Ranking Theory
So, assume we have:
- A benchmark document collection.
- A benchmark suite of queries.
- A binary assessment of either Relevant or Non-relevant for each query and each document.

This binary assessment sounds a lot like **a classification problem.**

So...
Classification Training:
- Given a training set of (query, doc, rel) triples, learn a model f.

Classification testing:
- Given unseen (query, document), apply f(query, document) and output Relevant or Non-relevant classification.

### Relevance classification example

Imagine having a dataset of the scores of document-query pairs, their different features $cos(q,d)$ and $w$, and their relevancy classification.

We can then plot them and apply a linear regression to create separating hyperplanes that linearly separate relevant and non-relevant across the graph. 

So now, if given new document 8, 9, or 10 we can predict their relevancy. 
(Example shown below)

![[Pasted image 20231209162505.png]]