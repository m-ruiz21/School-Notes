Whenever we run a query, we can get hundreds or even thousands of results. 
Users also often only view the first few results that are given, so we want to make sure that our search engine is capable of ranking and finding the most relevant results and make them quickly accessible to our users. 
## Scoring
So, let's build a scoring function that takes in a query and a document set.:
$$\begin{align} score(q,d) \end{align}$$
And lets suppose that the score ranges from \[0,1\].

The goal is going to be to score every document for a particular query with a scoring function that awards the highest scores to the best documents.

For example, if I wanted to have a ranking scoring algorithm for Cav's Algorhythms we could have:

$$ \begin{align} score(q,d) = (.1) popularity + (.2)album \end{align} $$

## Vector Space Model

**Big Idea:** Treat documents as queries as vectors in a high-dimensional space where our axes represent the content of our documents.
This content can be scoring factors (like we have previously) or, in this case, **terms**.

So if each vector axes represents the amount of instances of each term in each document, sort of like our original [[Class 02 - Search Basics#Term-Document Incidence Matrix|Term-Document Incidence Matrix]] from Class 02. 
Therefore, we can also see that the amount of axes in our vector space is the size of our dictionary.