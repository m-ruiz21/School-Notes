# Recap

[[Class 12- More ML Ranking|Last time]] we covered two classification approaches: Rocchio and kNN.

However, these don't outperform feature engineering. 
Also, predicting a query and document being Relevant and Non-relevant is a classification problem that's more similar to Boolean retrieval instead of ranking. 
So, we're not truly ML ranking *yet*.

# One Idea: Pointwise Learning

Assume we have training data like (query, document, *score*).

Here, *score* could be a relevance score like
0. Not relevant at all.
1. Somewhat relevant.
2. Relevant.
3. Very Relevant.
4. Perfect Match.

So now, instead of having a binary output, out goal is now to output a score, **making this now a regression problem** (if we can output any value) or **ordinal regression** (if we can only output 0, 1, 2, 3, or 4).

# Another idea: Pairwise Learning

The aim is to classify instance pairs as correctly ranked or incorrectly ranked. 

This turns an ordinal regression problem back into a binary classification problem in an expanded space. 

## Idea: Consider two docs!

Create a new space from pairs of documents:
$$ \Phi(d_i, d_k, q) = \Psi_i - \Psi_k $$
Where we combine the feature representations of each original representation $(d_i, q)$, $(d_k, q)$ to a new representation $\Phi(d_i, d_k, q)$.

If we output +1, then $d_i$ is preferred, else if we output -1 then $d_k$ is preferred. 