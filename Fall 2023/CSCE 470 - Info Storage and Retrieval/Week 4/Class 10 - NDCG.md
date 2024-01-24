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

## Types of Evaluations
- Offline - Usually with a standard dataset or using historical interactions from a production system like google.
- User Studies - Present search interface to a group of users (say 10-100), often in person or using a system like Amazon mechanical Turk. 
- Online - typically requires access to a production system with existing users. 
	- This might include something like A/B testing. 
