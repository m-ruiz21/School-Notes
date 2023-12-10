# Word2Vec Objective Function

Last time, we talked about [[Class 22 - word2vec|Word2Vec]]. 
We find that for each position $t=1, ..., T$ predict context words within a window of fixed size m, given a center word $w_t$. 
Data likelihood:
$$L(\theta) = \prod^{T}_{t=1}\prod_{ \underset{j \neq 0}{-m \leq j\leq m}} p(w_{t+j}|w_t;\theta)$$

The function that Word2Vec is hoping to optimize $J(\theta)$ , otherwise called the **objective function** or **loss function**, is the average negative log likelihood:

$$J(\theta) = -\frac{1}{T}log(L(\theta))$$

We want to optimize the objective function. 
So: **how do we calculate** $P(w_{t+j}| w_t;\theta)$? 
**Answer**: We will use two vectors per word $w$:
- $v_w$ when $w$ is a center word $\rightarrow w_{in}$ 
- $u_w$ when w is a context word $\rightarrow w_{out}$ 

Then for center word $c$ and a context word $o$:
$$P(o|c) = \frac{exp(u^T_o v_c)}{\sum_{w\in V} exp(u_w^T v_c)}$$

# Apply Word2Vec to IR (DESM)

**DESM**: A **Dual Embedding Space Model** for Document Ranking.

Answers the question: can we build a more intelligent ranker by using word embeddings like [[Class 22 - word2vec|Word2Vec]].

How does it do this? It builds on [[Class 08 - End TF-IDF#In practice|BM25]] model idea of "aboutness"
- But not just term repetition indicating aboutness, but rather the relationship between query terms and all terms in the document indicates aboutness. (BM25 only uses query terms)BM25 only uses query terms.

So the idea is that the document is represented by the centroid of its word vectors:
$$\bar{D} = \frac{1}{|D|} \sum_{d_j\in D} \frac{d_j}{||d_j||}$$

Thus, query-document similarity is average over query words of cosine similarity:
$$DESM(Q,D) = \frac{1}{|Q|} \sum_{q_i \in Q} \frac{q_i^T\bar{D}}{||q_i||\cdot ||\bar{D}||}$$

What works best is to use the OUT vectors for the document and the IN vectors for the query:

$$DESM_{IN-OUT}(Q,D) = \frac{1}{|Q|} \sum_{q_i \in Q} \frac{q_{IN, i}^T 
\overline{D_{OUT}}}{||q_{IN, i}|| \cdot ||\overline{D_{OUT}}||}$$

>IMPORTANT CONCEPT:

This way, similarity measure the **aboutness** - words that appear with this word - which is more useful in this context than (distributional) semantic similarity.

> AKA we want documents relating to the abstract context of the query not with a bunch of words relating to the definition query.

# Summary 

- DESM showcases one approach to incorporating word embeddings into a retrieval scenario.
- Not great at ranking documents, but better at reranking somewhat relevant documents according to "aboutness".

