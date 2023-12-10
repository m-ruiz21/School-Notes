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
