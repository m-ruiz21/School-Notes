## TF-IDF: Putting it all together
Putting our [[Class 07 - Ranking Functions#TF = term frequency|TF]] and [[Class 07 - Ranking Functions#IDF = Inverse Document Frequency|IDF]]  weighting strategies together, we can find the TF-IDF score of a given term $t$ and document $d$ within documents $D$:

$$\begin{align}tfidf(t,d,D) =tf(t,d) \cdot idf(t,D) \end{align}$$

## Overview:
So to quickly overview: we have two main types of weighting we use to populate the values of our vectors:
1. Raw count
2. TF-IDF

## In practice:
In practice, we can use a modern ranker called BM25:

$$\begin{align}
score(D,Q) = \sum^n_{i=1}IDF(q_i) \cdot
	\frac{tf(q_i, D)\cdot (k_1 + 1)}{tf(q_i, D) + k_1 \cdot (1-b + b\cdot \frac{|D|}{avgdl})}
\end{align}$$

Where:
- $k_1$ controls term frequency scaling.
	- $k_1=0$ is the binary model (Boolean term existence) and a large $k_1$ is raw term frequency.
- $b$ controls document length normalization
	- $b=0$ is no length normalization and $b=1$ is relative frequency.
	- Typically, $k_1$ is set around 1.2-2 and b is around 0.75

We can consider this as an advanced version of [[#TF-IDF Putting it all together|TF-IDF]].