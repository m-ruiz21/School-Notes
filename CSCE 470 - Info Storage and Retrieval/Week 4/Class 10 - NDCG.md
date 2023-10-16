This class is a continuation of the NDCG introduction from [[Class 09 - Evaluation#NDCG|Class 09]] 

**NDCG Equation**
$$\begin{align} nDCG_p = \frac{DCG_p}{IDCG_p} \end{align}$$

Where $DCG_p$ is the DCG of the top p returned documents and $IDCG_P$ is the ideal DCG of the top p returned documents.

We can find $DCG_p$ as follows:

$$\begin{align} DCG_p = \sum_{i = 1}^{p} \frac{2^{rel_i} - i}{log_2(i + 1)}\end{align}$$

Where $rel_i$ is the relevance level of item $i$. 

## Offline Evaluation Summary

We have mostly discussed offline evaluation, where we want to test a hypothesis (i.e. search engine x is better than old search engine y) 

Assumption we have a test collection of the following:
 - Docs (representative of our collection)
 - Queries (representative of what our users will / do ask)
 - Relevance judgements (can be expensive to collect and contain a lot of noise)
 - 